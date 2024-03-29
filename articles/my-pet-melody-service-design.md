---
title: "価値のありそうな1つの体験を主軸にすべてを考え、個人アプリ「うちのコメロディー」をリリースしてみました"
emoji: "🐈"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["個人開発", "uiuxdesign", "materialdesign"]
published: true
---

:::message
この記事は[個人開発 Advent Calendar 2023](https://qiita.com/advent-calendar/2023/personal-developement) の 21 日目の記事です。
:::

先日、「うちのコメロディー」というアプリをリリースしました。

https://twitter.com/colomney/status/1730919744558293034

まだ必要最小限の機能しかない価値検証のアプリ風のものですが、ファーストリリースまでにやったことと考えたことなどをメモしてみます。

技術的な話は以下にまとめましたので、こちらもよろしければどうぞ。

https://zenn.dev/colomney/articles/my-pet-melody-technologies

# 着想

私は趣味で作曲をしています。

そのことを知っていた知り合いの猫好きな方から、「ウチで飼ってる猫の鳴き声使って、オリジナルの音楽作れないか？」と話を持ちかけられました。

知り合いは元々、以下のような猫の鳴き声と音楽を組み合わせた作品を YouTube などで見たことがあったらしく、そこから着想を得たようです。

https://youtu.be/kG2JvYSqGR4

そうして、知り合いの猫の動画を共有してもらい、それを元にしたオリジナル音楽を何点か作りました。

https://youtu.be/wjyNe1lGZfU

オリジナル音楽を共有すると、知り合いはすごく喜んでくれました。
私の予想を遥かに上回り喜んでいる感覚を受けたので、喜んでいる理由をそれとなく聞いてみました。

知り合いいわく、自分で飼っている猫の「オリジナル作品」ができたというところに特に感動を覚えるということでした。

この際に、自分のペットだけのオリジナル音楽を作れるサービスは、面白いんじゃないかと着想を得ました。

# サービス設計に着手するまで

既存のサービスで同様のものがないかをまず調査しました。
1 つだけほぼ想定しているサービスと同じようなものを見つけましたが、すでにサービス終了していました。

https://www.itmedia.co.jp/dc/articles/1311/26/news148.html

元々、価値のありそうな体験をミニマムに提供するサービスを、ゼロから設計してリリースしたいというモチベーションがあったので、この時点で作ってみようと決意しました。

本当に需要がありそうかの検証はできていません。

# 最重要のユーザー体験

サービスを設計するにあたり、ユーザーにとって価値ある体験を以下のように仮定しました。

```
自分が飼っている猫の動画を用意するだけで、オリジナル曲が作れる。
```

これは前述の知り合いとの会話や経験を元に設定しました。

要件定義や UI/UX 設計の際には、ユーザーがこの「最重要の体験」を簡単かつすぐに得ることを最優先の目標として組み立てていきました。

# ペルソナ設定

最重要のユーザー体験に加えて、ターゲットとするユーザーのペルソナを以下に設定しました。

```
「猫」を飼って愛でていて、かつ、家族の一員として大切に育てている。
```

こちらも前述の知り合いとの会話や経験を元に設定しました。

要件定義や UI/UX 設計の際には、ペルソナにとって価値があるかどうかを意識して組み立てていきました。

# 要件定義

スマホで猫の動画を撮影した後にオリジナル曲を作るという流れを繰り返しやすくするため、モバイルアプリとして提供することにしました。
モバイルアプリは、初回利用時にストアからアプリをインストールする際に、ホーム画面にショートカットが作られます。
そのため、ユーザーが 2 回目以降アプリを開く動線が自然に作られるため、上記の狙いが達成しやすくなります。

全体の体験として、作品を作るためだけに猫の動画を撮影する必要がある場合、カメラを短時間に何度も向けることで猫にストレスを与えてしまう可能性があります。
このことは、猫を大切に育てているペルソナにとっては、嫌なこととなりえます。
そのため、すでに撮影している動画を使ってできるように全体の体験や UX を設計しました。

また、SNS へのシェア機能は必要と考えました。
ペルソナは猫を愛でていて、我が子だけのオリジナル作品を自慢したいという欲求が考えられるためです。

# デザインシステムの設計

モバイルアプリの技術として Flutter を使う前提だったので、Flutter で iOS/Android 両方ともに適用しやすい Material Design を踏襲することにしました。

https://m2.material.io/

ペルソナが気に入りそうな動物の温かみを感じるような世界観にしたかったため、コンセプトカラーを茶色に設定しました。

![](/images/my-pet-melody-service-design/color-palette.png)

画面のデザインは Material Design のものをベースとしつつ、オリジナル曲を作るフロー内のみタイトルバーを透明とし、動画選択などのアクションボタンが相対的に目立つようにしました。

![](/images/my-pet-melody-service-design/title-bar-of-design-system.png)

これらの画面では、迷わず先に進められることが重要であり、タイトルバーに表示されているテキストや戻るボタンは、動画選択などのアクションボタンよりも重要度が低いです。
ユーザーが迷う可能性を下げることで、最重要な体験に辿り着く可能性をあげることに寄与できると考えたため、上記のデザインルールを導入しました。

# イラスト

ペルソナが気に入りそうな可愛い雰囲気にしたいと考えたので、猫のイラスト製作をデザイナーに依頼しました。
イラストは描けないので、他の人の力を借りました。

あと、ただの思いつきですが猫がアニメーションして動くと可愛いなと思い、パラパラ漫画風にアニメーションできるように体勢や角度違いのイラストを複数枚描いてもらいました。

![](/images/my-pet-melody-service-design/flicking-image.gif)

# ユーザーテスト

プロトタイプが完成した直後にユーザーテストを実施し、ユーザーが操作している様子を横で観察することで、機能や UI/UX の課題を洗い出しました。
前述の知り合いに手伝ってもらいました。

「プロトタイプ完成後にユーザーテストを実施し、課題を洗い出してアプリを修正」というサイクルを 3 回程度繰り返しました。

オリジナル作品を作るにあたり、猫が映っている動画の中から鳴き声が入っている部分をトリミングする必要があるのですが、プロトタイプ時点では、アプリの外で動画の鳴き声をトリミングする想定でした。
ただし、ユーザーテストを行うと、その方法はかなり複雑な操作になることが分かり、最重要の体験前に脱落する原因となる可能性が高いと感じました。
そのため、アプリ内でトリミングする機能をつけました。

また、アプリ内でトリミングする際にも、ユーザーが自分の手で鳴き声部分を確認してトリミングするのは、かなり難易度が高いと感じました。
そのため、鳴き声を検知して自動でトリミングする機能をつけました。

:::message
鳴き声を検知して自動でトリミングする機能は技術的には難易度が高く、工数もかかるものでした。
ただ、ユーザーが迷わない UI/UX を設計する難易度の高さや最重要のユーザー体験までに脱落する可能性の高さなどと天秤にかけ、実施することにしました。
脳死でポチポチタップするだけで最重要の体験に辿り着けるというのは、メリットが大きいかなと思いました。
:::

さらに、プロトタイプ時点では、元々 2 つの動画を選んで 1 つの作品を作る、という機能を実装していました。
ところが、こちらも操作の流れが複雑になってしまい、最重要の体験までの脱落の原因となりうると感じました。
そのため、動画は 1 つのみを選択するようにして、全体の流れをシンプルにしました。

# サービス名

前述している通り、「うちのコメロディー」、英語名では「My Pet Melody」という名前に決定しました。

最重要のユーザー体験における、我が子のためだけのオリジナル音楽を作れることが名前から簡単に察せることを狙っています。

また、その他にも以下を考慮しています。

- 一瞬でぱっと読めるか
- 類似サービス名がないか
- すでに商標登録されていないか
- 英語名のドメインがとられていないか

# キャッシュポイント

アプリでは、無料プランと有料プランを用意し、それぞれで機能差をつけています。

キャッシュポイントを作ったのは、キャッシュポイントをつけることで要件定義や UI/UX 設計の複雑さが上がるため、その部分を勉強したいと考えたからです。
サービスとしての事情ではなく、個人のモチベーションが理由です。

無料プランでも最重要の体験を得られるようにし、もっと繰り返したくさん体験したいと感じてもらったタイミングで有料プランに誘導されるように、機能の制限を設計しました。

価格設定については、特に理由はなくテキトーです。

# 法務的視点

以下のサイトで、利用規約とプライバシーポリシーを作成し、そこからサービス特有の事情に合わせて少しカスタマイズしました。

https://www.cloudlegal.jp/contracts

また、オリジナル作品の BGM に使う予定の音楽に関して、著作権の状態を確認し、パブリックドメインとなっているものだけを利用するようにしました。

# マーケティング

作れる作品のイメージが湧きやすいような動画を作り、宣伝やストアの素材として利用しました。

https://youtu.be/uTSQPfuDNyo

# 展望

以上が、個人アプリ「うちのコメロディー」をリリースするまでにしたことすべてです。

現時点ではユーザー数はそこまでいなくて無風状態という感じですが、今後、以下あたりをぼちぼち試していければなと考えています。

- 宣伝時の謳い文句を変える
- できることの想像がつきやすいように宣伝方法を工夫する
- ターゲットのペルソナを変える（猫を飼っている人から、他の動物を飼っている人、育児中の家庭など）
- そもそも需要がなかったと分かったら、サービスを終了する
