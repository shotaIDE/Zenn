---
title: "多国籍チームでタッグを組み、継続的にスピード感ある価値提供ができるエンジニアリングを目指す"
emoji: "🕌"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["チーム開発", "要件定義", "リリース"]
publication_name: "sun_asterisk"
published: true
---

:::message
本記事は、[Sun\* Advent Calendar 2023](https://adventar.org/calendars/9043) の 12 日目の記事です。
:::

こんにちは。[Sun Asterisk](https://sun-asterisk.com/)でモバイルアプリエンジニアをやっている、井手 将太です。

私は普段、Sun Asterisk(以下 Sun\*と表記します)のモバイルアプリのプロジェクトに、技術リードやエンジニアリングマネージャー、プレイヤーなどとして参画しています。
今までの経歴としては、iOS ネイティブや Android ネイティブ、Flutter の 3 つをおおよそ均等に経験し、モバイル中心で歩んできました。

最近は、モバイルのプロジェクトに参画しながら、エンジニアがチームとして高いパフォーマンスを発揮し続けられるにはどうすればいいか、ということに対して色々試行錯誤しています。
なので、頭の整理を兼ねて、その辺りの話を書いてみます。

# 想定する読者

スクラム開発でプロジェクトを進めている、プロジェクトマネージャーや、エンジニアを想定しています。

# 現在取り組んでいるプロジェクトとその背景

Sun\*は、クライアントさんと一緒にチームを組んで、さまざまなプロダクトを届けることなどを通じて世の中に価値提供をしています。

私が取り組んでいるプロジェクトは、元々クライアントさんがリリースしていたサービスのリブランディングや開発の各種課題を解決したいというところからスタートしました。

サービスのブランディングに関しては、UI/UX の統一やブランディングの確立ができておらず、ユーザーに訴求しにくいものとなっていたという課題がありました。
また、開発の各種課題に関しては、**技術的負債が蓄積していて、デリバリーサイクルが長期化している**という課題がありました。

上記の課題を解決するために、Sun\*がジョインし、デザイン面とモバイルアプリの開発面で一緒にチームを組んで課題解決を進めております。

私は、**モバイルアプリの開発チームとしてジョイン**しています。
そうした状況の中で、モバイルアプリの開発チームが開発スピードを維持しながら継続的に価値提供していくために取り組んでいる内容を紹介します。

# 現在のプロジェクトにおける多国籍チームでタッグを組む際の制約

Sun\*はベトナムの拠点に 1000 名以上のエンジニアが在籍しており、潤沢な開発力があります。
ベトナムのエンジニアチームは、ある程度曖昧な要件に対しても積極的に細部をディスカッションして詰めて開発を推進していけるような、開発のプロフェッショナルチームです。
そのため、特に「開発スピードを維持して継続的に価値提供する」ということにも自立して考え、取り組んでくれます。

私が取り組んでいるプロジェクトにおけるモバイルアプリの開発チームでも、ベトナムのエンジニアに iOS、Android、QA それぞれ 5 名程度ずつジョインしてもらい、開発を推進してもらっています。
加えて、日本のメンバーも PM やエンジニア合わせて 4 名程度ジョインして、モバイルアプリの開発チームという形をとっています。
その他、Sun\*のデザインチームや、クライアントさん側のプロダクトチーム、QA チーム、API 開発チームなどがあり、これらのチームと協力してプロジェクトを進めています。

このようにベトナムメンバーと日本メンバーでタッグを組む際に注意するポイントの 1 つは、**日本語を話すクライアントさんや日本語を話す他のチームと言語の壁がある**ということです。

![](/images/continuous-delivery-by-multinational-team/language-barrier.png)

開発スピードを維持して継続的に価値提供するという命題は、開発チーム内だけで完結して実現可能なものではありません。
状況に応じて、**デザイナー、ビジネスサイド、サポートチームなどを巻き込んでいく必要がある、複雑な問題**です。
そのため、ベトナムの開発メンバーと、日本語を話す他のチームとの連携は必要になってきます。

このために、**開発チームのベトナムメンバーと日本メンバー間の口頭でのコミュニケーションを密に取る**ことで、日本語を話す他のチームとの橋渡しをうまく実施していく方法が考えられます。
ただし、この方法は**使用頻度が高くなりすぎないよう気をつける必要があります**。

ベトナムメンバーと日本メンバーは、オンラインミーティングでブリッジ SE という役割の方の通訳を通して口頭でコミュニケーションをとれます。
この際、通訳という処理が入るため、コミュニケーションの場としてのフロー効率は悪く、時間を多く消費してしまいます。
そのため、あまりにこの時間をとってしまうと、長時間ミーティングが増えてしまい、メンバーが疲弊してしまうという問題が発生します。

![](/images/continuous-delivery-by-multinational-team/translation-flow-efficiency.png)

そのため、**コミュニケーションパスを制限し、取り決めによりお互い干渉せずに各々業務を進めるという選択肢を取れるようにしておく**ことも重要です。

# 業務ドメインの分担

開発スピードを維持して継続的に価値提供するためには、さまざまな開発における業務ドメインに取り組む必要があります。

それらをベトナムチームと日本チームで分担、連携しながら進め、時には分担ややり方を変えるなどの試行錯誤をしてきました。

プロジェクトが開始してから 1 年程度経過し、ある程度、業務ドメインごとの効率的な境界線や連携方法が見えてきました。

現在、以下のような分担や連携をしています。

![](/images/continuous-delivery-by-multinational-team/domain.png)

# 業務ドメインの分担や連携の背景や意図

全ての業務ドメインの担当や連携に関して試行錯誤や理由、意図などがあります。
ここでは、ベトナムチームと日本チームでタッグを組むという状況を踏まえた時に、特に注目していただきたい内容をピックアップして記載していきます。

## 要件定義

要件定義は、基本的に日本チームとクライアントさんのプロダクトチームとの間で行います。
一方で、ベトナムチームからフィードバックをもらった際にすぐに軌道修正できるよう、**日本チームだけで詳細に決めすぎないようにしています**。

日本チームにも私がエンジニアとして入っているので、ある程度の技術的な実現可能性や、メンテナンス性とのバランスを取った要件定義を進めることができます。
ただし、ベトナムチームの実際にコードをメンテナンスしているメンバーと、日本チーム側の私との、理解しているコードの情報量の差がどうしてもあります。
そのため、実際に設計や実装してから初めて要件における不備が発見されることもあります。

そうした状況を事前に防ぐことは困難なので、**素早く軌道修正できるようにすることを重要視**しています。

![](/images/continuous-delivery-by-multinational-team/feedback-by-development-team.png)

具体的には、達成したいことや概要設計あたりくらいまでは日本チームで定めて、実際のアーキテクチャーを踏まえた詳細設計レベルから先はベトナムチームに任せています。

一方で、要件定義に至るまでの周辺状況や背景、意図などは、明確に明文化して伝えるということに取り組んでいます。
背景知識まで伝えることで、ベトナムチームのメンバーも「提示された仕様や概要設計がプロダクトにとって妥当か」という点まで考えることができ、より良い設計の提案などを実施してくれます。

:::message
要件定義においては、ベトナムチームのブリッジ SE も一緒に参加してもらうという手段があります。
これにより、ブリッジ SE からベトナムの開発メンバーに要件やその背景を直接伝えることができるため、齟齬が生じにくくなるというメリットが考えられます。
本プロジェクトでは、ブリッジ SE が要件定義のミーティングに参加することで他の作業時間が圧迫されるデメリットと、齟齬の実際の発生リスクのバランスを考慮し、この方法を基本的に採用していません。
:::

## タスクの見積もり

タスクの見積もりは、**ベトナムチームと日本チームがオンラインミーティングへ一緒に参加して実施**しています。

![](/images/continuous-delivery-by-multinational-team/estimate.png)

元々見積もりは、仕様を日本チームが明文化し、それを見てベトナムチームがストーリーポイントを見積もるという分担方法を採用していました。

ただ、進行するにつれて、**ベトナムチームの見積りと日本チームの想定の間で乖離**がよく見られるようになりました。
これには、タスクの達成したいことの認識が合っていない、既存コードとの兼ね合いによるコストの見通しが合っていない、などが原因でした。

これらの課題を解決するため、ベトナムチームと日本チームが一緒にプランニングポーカーを行い、**認識のずれをその場で解消する方式に変えました**。

一方で、オンラインミーティングで行うため、時間の関係上細部まですり合わせることが難しいです。
そのため、正確な見積もりができないことに対する不安をベトナムチームが感じ、方法を変えることに対する反発が少しありました。

しかし、時間を過剰にかけて正確な見積もりを出しても、このプロジェクトにとっては費用対効果が薄いです。
また、見積もりが大きくずれてしまった場合、デイリーの確認でそのずれを認知し、スプリントゴールを調整すればあまり問題になりません。

これらのことをベトナムチームに伝えて、納得してもらい、変更後の方法で運用することになりました。

## リリース作業

リリース作業は、プロダクトチームやクライアント側の QA チームとの細かい調整が必要になってくるので、**日本チームだけで実施できるようにしています**。

![](/images/continuous-delivery-by-multinational-team/trunk-based-development.png)

トランクベース開発を採用し、**トランクブランチはどのコミットでもリリース可能な状況**となるよう、ベトナムチームとコミットの粒度やゴールを認識合わせしています。

https://cloud.google.com/architecture/devops/devops-tech-trunk-based-development?hl=ja

長い期間にわたって複数の PR がマージされることで完成するような大きい機能に関しては、フィーチャートグルを導入しています。
これにより、**機能完成までの PR が全て揃っていない状態でもリリースできます**。

https://ja.wikipedia.org/wiki/%E3%83%95%E3%82%A3%E3%83%BC%E3%83%81%E3%83%A3%E3%83%BC%E3%83%88%E3%82%B0%E3%83%AB

上記の状況では、**ベトナムチームはトランクブランチへマージすることに集中**し、**日本チームはリリース時期にトランクブランチ上で検証が完了しているコミットまでをリリース**すれば良くなります。
これにより、リリースに伴う作業のための、ベトナムチームと日本チームの密なコミュニケーションが不要となります。

## 開発プロセスの評価

**ベトナムメンバーの定性的な自己評価**や、**ベトナムチーム内でのスプリントごとの振り返りを日本チームに共有**してもらうことで、開発プロセスにおける改善の妥当性や問題点の洗い出しを行っています。

定性的な自己評価では、Google フォームにより作成したアンケートに対し、 2 ヶ月に 1 回回答してもらっています。

![](/images/continuous-delivery-by-multinational-team/qualitative-research.png)

内容としては、**開発チームのコード、各種開発プロセスや、チームに対する満足度**などに対する評価ポイントや自由記述の意見などを回答してもらっています。

これらの質問は、DevOps の能力や、SPACE 指標を参考に作成しています。
測定したいキャパシティや指標を設定し、それらが測定できるように質問を構築しています。

https://cloud.google.com/architecture/devops?hl=ja

https://queue.acm.org/detail.cfm?id=3454124

スプリントごとの振り返りでは、**「感謝したいこと(Thanks)」「課題(Issue)」の 2 分類**で意見を出す単純なフレームワークなどを利用し、ベトナムチーム内で実施してもらいます。

![](/images/continuous-delivery-by-multinational-team/retrospective.png)

「感謝したいこと」を組み込んでいる意図としては、メンバーが「良い」とか「楽しい」と感じる基準を間接的に読み取ることができると考えたからです。
これにより、開発プロセスの改善や業務ドメイン分担などにおいて、メンバーのモチベーションにつながる取り組みへ繋げることができます。

振り返りは Miro で実施しているので、**意見などが書かれたベトナム語の付箋を日本語に翻訳してもらい、ブリッジ SE の方に口頭の補足踏まえて内容を共有してもらいます**。

定性的な自己評価では、複数人からコードの内部品質に関して特定のトピックを改善したいという意見が上がってきました。
振り返りなどで詳細をヒアリングし、スプリント計画に組み込んでいます。

また、振り返りなどで、新しい技術を習得することをポジティブに捉える意見が継続的に出ていました。
ベトナムチーム内で不足している知見をレクチャーして、新しい技術を習得してもらうという機会を定期的に作っています。

# まとめ

以上のように、多国籍チームでプロジェクトを進めていく際は、多国籍チームならではの制約を踏まえた上で、業務ドメインを適切に分担、連携していく必要があります。

上記で、私たちが実施している取り組みを紹介しましたが、これは、あくまで現時点での試行錯誤の結果のスナップショットにすぎません。
今後も進めていく中でブラッシュアップしていくことで、開発スピードを維持した継続的な価値提供を実現できると考えています。

これらの情報が、同じような状況でチャレンジされている方々の参考になれば幸いです。
