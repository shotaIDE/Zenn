---
title: "ライブラリ更新に時間かかりすぎて、更新作業だけで人生終わっちゃうという危機感を持つ人に送る！"
emoji: "🎃"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["flutter", "ios", "android"]
published: false
---

<!-- cspell:ignore automerge, noreply, podfile, precache, subosito, temurin -->

# はじめに

アプリ開発で、運用やメンテナンスにかかるコストはできるだけ削減することが重要です。

特に、ライブラリの更新は、アプリの品質を保つために欠かせない作業の一方で、その更新作業自体がコストを生むことがあります。

本記事では、Flutter プロジェクトでライブラリの更新を自動化する方法について紹介します。

# 概要

Renovate を導入し、PR 作成を自動化します。
これにより、Flutter のライブラリの依存関係定義ファイルとロックファイルが更新された PR が作成されます。

CI により、Flutter のライブラリが間接的に利用する iOS ネイティブのライブラリのロックファイルを更新し、PR にプッシュバックします。

Renovate の自動マージにより、マージされます。

# 詳細

## 前提

GitHub で開発し、GitHub Actions で CI を組んでいる前提で説明します。

ライブラリの更新 PR は、**1 ライブラリにつき 1PR** としています。
ただし、Renovate の設定により、複数ライブラリを 1PR にまとめることも可能です。

また、本記事で前提としているのはアプリ開発です。
そのため、ライブラリの**新しいバージョンがリリースされたら、できるだけ早く最新のバージョンのみを利用するようバージョン指定の制約を更新**するようにします。

:::message
一方ライブラリ自体の開発では、そのライブラリが利用するライブラリのバージョン制約は広く取り、制約の更新自体も緩やかに行うことが一般的です。
これは、他の人やチームから様々な状況において利用されることを考慮しているためです。
本記事では、ライブラリ自体の開発においては適していない方法になっています。
:::

## Flutter のライブラリ依存関係の定義方法を変更

`pubspec.yaml` におけるライブラリのバージョン指定は、キャレット演算子 `^` を使うことが一般的です。

一方で、ライブラリ開発ではなくアプリ開発においては、新しいバージョンの依存関係のライブラリがリリースされたら、すぐに最新版に更新することが望ましいです。

ただ、Renovate は `pubspec.yaml` のバージョンを見て更新 PR を提出するか否かを決定します。

そこで、記載されているライブラリのバージョン絶対指定に変更します。

```diff yaml:pubspec.yaml
name: app_name
description: App description.
publish_to: "none"
version: 1.0.0+1

environment:
  sdk: ">=2.18.5 <3.0.0"
  flutter: ">=3.19.5"

dependencies:
-  cloud_firestore: ^4.15.10
+  cloud_firestore: 4.15.10
-  collection: ^1.18.0
+  collection: 1.18.0
# ...
```

## Renovate の導入

Renovate は、GitHub のリポジトリにプルリクエストを作成し、ライブラリの更新を自動化するツールです。

https://docs.renovatebot.com/

以下の "Hosted GitHub.com App" を参考にして、GitHub App として該当のリポジトリに対してインストールします。

https://docs.renovatebot.com/getting-started/installing-onboarding/#hosted-githubcom-app

## Renovate の設定

Renovate をリポジトリにインストールしたら、ライブラリ自動更新の推奨設定が適用された PR が提出されます。

![](/images/automatically-upgrade-flutter-dependencies/renovate-configure-pr.png)

そのままマージはせず、適した設定に修正します。

以下のように設定しています。

```json:renovate.json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "enabledManagers": ["pub"],
  "packageRules": [
    {
      "matchManagers": ["pub"],
      "automerge": true
    }
  ],
  "prConcurrentLimit": 4
}
```

`prConcurrentLimit` は、同時に提出される PR の数を制限するための設定です。
PR が同時に大量に発生してノイズにならないように、適切な数に設定すると良いです。

このように修正後、PR をマージします。

## iOS ネイティブのライブラリのロックファイルを更新し、プッシュバックする

プッシュバックした後に CI がトリガーされるように、パーソナルアクセストークンを用意します。

プロジェクト運用上 GitHub Apps で作成したアクセストークンを使う方が良いですが、今回は一番簡単な個人のアクセストークンを使う方法をご紹介します。

リンクです。

`GH_PERSONAL_ACCESS_TOKEN` としてアクセストークンを登録しておきます。

次に、ワークフローを作成します。

```yaml:.github/workflows/ios.yml
name: CI / iOS

on:
  pull_request:
    branches:
      - "main"

concurrency:
  group: ${{ github.workflow }}-${{ github.head_ref }}
  cancel-in-progress: true

permissions:
  contents: read
  pull-requests: write

jobs:
  push-back-diffs-if-needed:
    name: Push back diffs after resolving dependencies if needed
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          ref: ${{ github.head_ref }}
          token: ${{ secrets.GH_PERSONAL_ACCESS_TOKEN }}
      - name: Setup Git
        # Git のユーザーとして "github-actions[bot]" を設定する
        # https://github.com/actions/checkout/issues/13#issuecomment-724415212
        run: |
          git config --global user.email "41898282+github-actions[bot]@users.noreply.github.com"
          git config --global user.name "github-actions[bot]"
      - uses: actions/setup-java@v4
        with:
          distribution: "temurin"
          java-version: "17"
      - uses: subosito/flutter-action@v2
      - name: Install iOS dependencies
        run: |
          flutter pub get --no-example
          flutter precache --ios
          cd ios
          pod install
      - name: Commit
        run: |
          git add ios/Podfile.lock
          if git diff --cached --quiet; then
            echo "No changes to commit"
          else
            git commit -m 'build: fix Podfile.lock'
          fi
      - name: Push back if needed
        run: |
          BRANCH_NAME="${{ github.event.pull_request.head.ref }}"
          git push origin "$BRANCH_NAME"
```

# 実際に動作している様子

Renovate が PR を作成します。

![](/images/automatically-upgrade-flutter-dependencies/pr-by-renovate.png)

最初は以下のようなコミットが作成されます。

![](/images/automatically-upgrade-flutter-dependencies/first-commit-by-renoate.png)

以下のようなコミットがプッシュバックされ、CI がトリガーされます。

![](/images/automatically-upgrade-flutter-dependencies/push-back-commit.png)

CI がパスすると、以下のように PR がマージされます。

![](/images/automatically-upgrade-flutter-dependencies/auto-merge-by-renovate.png)

# まとめ