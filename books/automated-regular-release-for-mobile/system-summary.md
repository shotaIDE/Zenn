---
title: "仕組みの概要"
free: true
---

大きく分けて以下の 2 つのサイクルにより仕組みを実現します。

- メインブランチにライブラリ更新が定期的にマージされるようにしておく
- 自ら定義した頻度で自動リリースの処理を動かす

# メインブランチにライブラリ更新が定期的にマージされるようにしておく

以下の要素を組み合わせて、ライブラリ更新が品質を保った状態で定期的にマージされるようにしておきます。

- ライブラリ更新の PR が自動で作成されるようにする
- 静的解析と単体テストがパスすることを PR のマージに必須の条件とする
- PR のマージ必須条件が満たされた場合、自動でマージされるようにする

# 自ら定義した頻度で自動リリースの処理を動かす

以下のようにフローを組みます。

![](/images/automated-regular-release-for-mobile/automated-release-flow.png)

以下の要素を組み合わせています。

- スケジュールで定期的に自動リリースの処理をキック
- データストアを見て前のリリースの審査中ではないかを判定する
- 前回のリリースから差分があるかを判定する
- E2E テスト実行
- データストアにリリースの審査中とマーク
- 商用アプリをデプロイ＆審査提出
- 審査が通り公開された際に、データストアにリリース済みとマーク

トリガーの頻度は変数なので、どの程度の頻度でリリースしてもいいかを元に決定します。
