## 基本情報

|key|value|
|---|-----|
|Name|柴谷遼太朗|
|GitHub|[@shibatani](https://github.com/shibatani/)|
|Zenn|https://zenn.dev/shibari_yo|
|Wantedly|https://www.wantedly.com/id/ryotaro_shibatani|


## スキル
### 言語
|言語|経験年数|レベル|
|---|-------|-----|
|Ruby|1年|基本的なプログラミングが可能|
|JavaScript|2.5年|人に教えれるレベル|
|TypeScript|2.5年|人に教えれるレベル|

### フレームワーク

|フレームワーク|経験年数|レベル|
|---|-------|-----|
|Ruby on Rails|1年|基本的な使用が可能|
|Vue.js|1.5年|実務で問題なく使える|
|Nuxt.js|1.5年|実務で問題なく使える|
|React|1年|実務で問題なく使える|

# 職務経歴  

## 2022/10 - 現在 : 株式会社ビットキー

## PJでの主な役割
- オフィスビル向けプラットフォームサービスの新規開発および既存機能改修

## 環境
- チーム規模: 36人 (フロント/バックエンドエンジニア 16名, インフラエンジニア 1名, アプリ開発エンジニア 5名, SRE/インフラエンジニア 3名, QAエンジニア 3名, UI/UXデザイナー 3名, データエンジニア 1名, PO 3名)
- 役割: フロント/バックエンドエンジニア
- 使用技術: TypeScript, Node.js, React.js, Github, Github Actions, Docker, Jest, GCP, Firebase, AlloyDB

## 業務内容
- フロント/バックエンドエンジニアの開発エンジニアとして参画
- 主にデータセンター向け機能の開発に従事
- 顧客からの問い合わせ調査・対応
- 定期リリース・定常業務対応
- 新規参画者へのオンボーディング・サポート

### データセンター向け機能の開発・導入
  - 概要

    データセンターのオペレーションは、サーバラックの予約、来訪者入退館時の受付対応、サーバラックまでのアテンド、サーバラックの解錠など多岐に渡る。そのようなオペレーションを安定的に運用しつつ、出来るだけ自動化したいという顧客要望がある。それらを実現するために新規機能開発・システム導入を行なった。
  - 取り組み
   
    まず、厳密な入退館管理を実現する必要があるため、申請機能を作成して承認済みのユーザーのみ入退館を行えるようにした。また、自動受付システムを導入して、入退館処理、サーバラックを解錠するICカードへの権限付与/削除を無人で行えるようにした。
### 大量予約処理の速度・パフォーマンス改善
 - 概要

   データセンターの規模拡張に伴い、一括予約できるサーバーラック数、予約への参加者数の上限を大幅に引き上げたいという顧客要望があった。現状のシステム構成だと、予約作成に時間がかかってしまい、現実的な運用がままならない。そのため、一括予約導線の速度改善を行う必要があった。
 - ボトルネックについて

   結論、予約処理内で叩かれる取得APIのパラメータが、大量予約によって重複し、リクエストURL制限で処理落ちしていたことが原因。予約作成処理自体は、Cloud Taskで非同期処理されており、リトライタスク作成と処理実行に時間がかかっていた。
 - 取り組み

   取得APIのパラメータ重複を取り除くことで、ボトルネックの改善を行なった。また、Cloud Taskの実行時間を少しずつずらすことによって負荷分散を行なった。結果的に、負荷分散しつつ予約処理の速度を 1/10に改善した。
### フロント画面の速度・パフォーマンス改善
- 前提

  大規模なRESTful API開発に対応するため、主に使用しているCloud Functionsから Cloud Runへ移行しようとしている。また、DBもFireStoreからRDBへ移行しようとしている。
そして、各サーバレス実行環境のregionは以下になる。

  - Cloud Functions → US
  - Cloud Run → Asia / US

  また、各DBのregionは以下になる。
  - FireStore→ US
  - RDB → Asia
- 取り組み

  実行環境はCloud Functions(US)側で、RDB(Asia)から情報を取得する汎用的なAPIが存在した。実行環境をCloud Functions(US)からCloud Run(Asia)に移行することにより、レイテンシ文脈で2画面の初期ローディング時間を削減した。速度改善結果は以下。
  - 画面①: 100件分データ取得の初期ローディング時間 1/3に
  - 画面②: 100件分データ取得の初期ローディング時間 1/6に

### 品質の改善
- 取り組み

  開発組織全体として、バグチケット数、顧客からの問い合わせ数が横ばいであることを問題視している。また個人的にも、データセンターへのシステム導入後の問い合わせ対応に忙殺されており、辛さを感じていた。
そのような課題に対して、以下のようなルールを個人的に設定し、品質の向上に努めた。

  - バックエンドの修正: 単体テスト&結合テストを必ず書く
  - フロントエンドの修正: ロジック部分のテストを必ず書く

  結果としてQA検証で、1チケットあたりのMajor以上のバグ発生率が、チーム平均で約40%だったのに対し、自分の対応に関しては約15%に留まった。

### スペース向け満足度機能の開発
- 概要

  社内のレイアウトや什器の配置、美化、備品の充実などを元に、従業員に働きやすい環境や空間を提供することを業務とするファシリティマネージャが企業によって存在する。  
そして、各企業のファシリティマネージャは、管理スペースの課題を洗い出し、改善する必要があるが、ワーカーが「実際にどのようにオフィス空間を利用しているか」というファクトの情報が集まりにくい課題がある。そのため、スペース向け満足度機能を作成して課題解決を試みる。
具体的なユースケースは、以下のようになっている。

   - ①満足度アンケートのスペース対象/アンケート回答者の範囲を設定する。
   - ②予約終了後、満足度アンケートを利用者にPush通知で送信。
   - ③Push通知を受け取ったワーカーがアプリで満足度を回答する。
   - ④ファシリティマネージャが管理画面で回答結果を確認し、改善に役立てる。
- 取り組み

  開発担当としては、要件定義、テーブル設計、I/F開発に従事した。開発組織全体として、大規模なRESTful API開発に対応するため、主に使用しているCloud Functionsから Cloud Runへ移行しようとしている。また、DBもFireStoreからRDBへ移行しようとしている。そのため、Cloud Run/RDBを利用して開発を行なった。また、他領域の開発については、複数人の業務委託メンバーに委託しており、進捗管理などを含むマンバーマネジメントも同時に行った。結果として、開発開始から納期まで1ヶ月というタイトなスケジュールであったが、期待された品質でプロダクトを作り上げることができた。
- 工夫した点

  テーブル設計、I/F設計については、以下を意識して行った。
   - 将来的にスペース対象以外の満足度も計測することを考慮してDB設計する
   - 紐づく外部データが削除されている場合でも、満足度データが積み上がっていくようにDB設計する
   - 集計結果を管理画面に表示させる必要があり、速度的な問題が発生しないようにクエリ設計する
   - 品質を担保するために、開発した全I/Fに対してユースケースに即したテストを書く
   - 問い合わせ工数削減を目的に、適切な粒度でレベルに応じたログを仕込む。

## 2020/12 - 2022/09 : 株式会社iRidge

## 家具・インテリア用品系アプリのCMS開発

### PJでの主な役割
・家具・インテリア用品系最大手会社様のCMS画面新規開発および既存機能改修
・アプリから呼び出されるWebView画面の既存機能改修

### 環境
- チーム規模: 10人 (フロントエンドエンジニア 1名(自分), バックエンドエンジニア 2名, インフラエンジニア 1名, Androidエンジニア 2名, IOSエンジニア 2名, PM 4名)
- 役割: フロントエンドエンジニア
- 使用技術: TypeScript, Vue.js/Nuxt.js, HTML, CSS, SCSS, Stylus, Pug, AWS(S3), GitLab CI

### 業務内容
- フロント側のメインエンジニアとして参画。
- PMおよび発注側とコミュニケーションを取りながら作成。
- PM側からの技術的相談にも対応。
- 工数見積もりにも対応。
- その他既存機能改修。

#### メンテナンスモード・強制アップデート管理画面の作成
  - 概要

    以前、PM側でモバイルアプリのメンテナンスモード・強制アップデートについてFirebase上で操作する必要があった。それらの作業を管理画面上で完結できように専用の管理画面を作成した。
  - 取り組み

    メンテナンスモード管理機能については、メンテナンス期間・メンテナンス時にアプリ側で表示されるテキストメッセージを設定できるようにした。 強制アップデート機能については、IOSもしくはAndroidの対象Ver・メンテナンス時にアプリ側で表示されるテキストメッセージを設定できるようにした。アプリ側では、対象Ver未満のアプリに対してアップデートを促すダイアログが表示される。
  - 工夫した点

     メンテナンスモードもしくは通常モードか一目でわかるように「状態」欄を作成した。さらにメンテナンスモード時には、赤色基調の文字色を使用し、主張するように工夫した。
       また、初めてシステムを使用した人がわかりやすいように使い方マニュアルリンクをページ内に配置し、モーダルで表示されるよう工夫した。

#### 重要なお知らせ管理画面の作成
  - 概要

    コロナにおける店舗営業時間の変更アナウンスや商品問題など緊急性の高い重要なお知らせをユーザー全体に発信する。CMS側では、それらのお知らせ内容を管理する画面を作成した。
  - 取り組み

    投稿画面では、表示日付・お知らせ内容・お知らせ内容の文字色・サムネイル・Draft状態かどうか・掲載期間・URLなどを設定できるようにした。
また一覧画面では、掲載予定・掲載期間中・過去の画面のように時系列に分けて管理できるようにした。
  - 工夫した点

    一覧画面ではお知らせ数が膨大になることを加味して、ステータスやタイトルなどでの絞り込みや掲載期間順にソートできるように工夫した。追加で顧客の要望に応え、選択した記事をCSV抽出できるようにした。また、同じような画面構成で作成されている既存一覧画面に対して、これらの機能を転用して使いやすくするように努めた。

#### トップバナー管理画面の作成
  - 概要

    アプリのトップ画面で表示される複数のバナーをCMS側で管理できるようにした。
  - 取り組み

    管理画面では、バナーのサムネイル・URL・表示するかどうかなどを設定できる項目を複数作成した。
  - 工夫した点

    サムネイルに表示する画像を大きさ・縦横比に関わらず全体表示できるように既存ライブラリ(Element UI)を使用して工夫した。

#### Node 12系→16系&サードパーティライブラリのアップデート
  - 概要

    Node 12系のLTS終了前にアクティブLTSである16系にアップデートした。またそれらに伴い、サードパーティライブラリのアップデートも行った。
  - 取り組み・大変だったこと

    サードパーティライブラリについては、ほぼ全て最新安定版にアップデートした。その中でも`eslint`、`date-fns`のバージョンが特に遅れており、記述の変更が大変だった。また、他ライブラリの依存関係において最新安定版で機能しないライブラリが存在し、それらの依存関係解消に時間がかかった。

#### リリース・オンボーディング関連のドキュメント作成
  - 概要

    以前はスポット的な対応が多かったため、継続的にPJに参加するフロントエンドエンジニアがおらず、あまりドキュメント類が整備されていなかった。特にリリース・オンボーディング関連のドキュメントが存在せず、次の新規参画者が路頭に迷うと考えたため、開発の合間にドキュメントを作成した。
  - 取り組み

    リリース関連については、フロントエンドのNotionページの中にリリースノート置き場を作成した。また、リリースノート雛形を作成し、テンプレート化させて次回リリースに使いまわせるように工夫した。Gitlab上でもリリースVerのタグ付けを行い、いつでもリリース内容を振り返れるように改善した。
  オンボーディング関連については、環境構築ページを作成してCMS、WebViewの立ち上げに必要な情報を記載した。

## 観光系Web版アプリの開発

### PJでの主な役割
鉄道系会社様が運営する観光系Web版アプリの既存機能改修

### 環境
- チーム規模: 10人 (フロントエンドエンジニア 3名, デザイナー 2名, バックエンドエンジニア 2名, Android/IOSエンジニア 1名, PM 2名)
- 役割: フロントエンドエンジニア
- 使用技術: JavaScript, Node.js/Express, HTML, CSS, SCSS

### 業務内容
- フロント側のメインエンジニアとして参画。
- PMおよび発注側とコミュニケーションを取りながら作成。

#### Web版アプリのレスポンシブ化対応
  - 概要

    以前Web版アプリは、PC画面のみ対応しておりSP画面に対応していなかった。
それらの解消にあたり、対応する画面数が膨大なため3人のエンジニアで担当画面を分割して対応を行った。
    
  - 取り組み

    対応の詳細な流れとしては、以下のように進めた。
    ①PM、デザイナー、エンジニアで対応する画面を決める。
    ②デザイナーがデザイン案をXDにまとめる。
    ③それらを元にエンジニアが対応する。

    エンジニアの具体的な対応方法としては、画面幅768px以上をPC画面、それ以下をSP画面としててスタイルをあてるようにした。また、スタイリングはBEMに準じて行うように共通認識を合わせて案件に取り組んだ。

  - 工夫した点

    エンジニア3人で担当画面を分割して対応するため、共通スタイルが絡むタスクを優先的に片付けるように工夫した。また対応する画面数が膨大なため、実装途中で要件が定まっていない箇所がいくつか出てきた。それらに関してデザイナーさんと直接話し合い、その場で要件を決めて迅速に対応した。

#### Node 12系→16系&サードパーティライブラリのアップデート
  - 概要

    Node 12系のLTS終了前にアクティブLTSである16系にアップデートした。またそれらに伴い、サードパーティライブラリのアップデートも行った。
  - 取り組み・大変だったこと

    サードパーティライブラリについては、ほぼ全て最新安定版にアップデートした。その中で`scss`のバージョンアップデートに伴い、ほぼ全てのscssファイルの記述を変更する作業が発生して苦労した。
    
## 鉄道系アプリのWebView開発

### PJでの主な役割
鉄道系モバイルアプリで表示するWebView作成。

### 環境
- チーム規模: 13人 (フロントエンドエンジニア 2名, バックエンド/インフラエンジニア 1名, モバイルエンジニア 2名, QAエンジニア 2名, デザイナー 2名, PM 4名)
- 役割: フロントエンドエンジニア
- 使用技術: TypeScript, Vue.js/Nuxt.js, HTML, CSS, SCSS, GitLab CI

### 業務内容
- フロント側のメインエンジニアとして参画。
- PMおよびデザイナーとコミュニケーションを取りながら作成。
- 既存機能の修正
  - イベントトラッキング対応

#### キャンペーン・スタンプラリー画面のUI/UX改善
  - 概要

    今後、鉄道会社様の方で多数のキャンペーン・スタンプラリー企画を計画しており、画面内にバナーが乱立することによって、ユーザー自身の興味のあるキャンペーン・スタンプシートに簡単にアクセスすることが出来なくなってしまう恐れがあった。画面のUI/UXを改善することによってこれらの問題を解決した。
  - 取り組み

    以前の画面は、キャンペーン項目とスタンプラリー項目を分ける事なく、上から順番にバナーを並べる構成だった。それらを変更し、画面上部はキャンペーン項目のスペース、画面下部はスタンプラリー項目のスペースに分け、それぞれの項目のバナーをスライダーでスワイプできるようにした。
  - 苦労した点

    スライダー間の幅や次スライダーをはみ出して見せるデザインなどの細かい表現をできるだけXD通りに再現できるように実装した。また、ページネーション部分が画面幅を変えることによってスタイル崩れが起こしていたが、スタイルのあて方を工夫することによって解決することができた。

#### 駅に基づく他社連携画面の作成
  - 概要
 
    ユーザーのお気に入り駅に紐づく他社連携画面を作成した。
  - 取り組み

    他社連携データに応じてボタンリンクを画面内に配置する。他社路線データが存在する場合は、他社アプリの列車走行位置リンクを配置し、バス/2次交通データが存在する場合は、HPリンクを配置するようにした。

## 銀行系Webサイトのデモ開発

### PJでの主な役割
銀行系Webサイトのデモ開発

### 環境
- チーム規模: 2人 (フロントエンドエンジニア 1名,  デザイナー 1名)
- 役割: フロントエンドエンジニア
- 使用技術:  HTML, CSS, JavaScript, jQuery  GitLab

### 業務内容
- メインエンジニアとして参画。
- デザイナーとコミュニケーションを取りながら作成。
- 工数の見積もりを担当。

#### 銀行系Webサイトのデモ開発
  - 概要

    依頼会社様にフロント系・デザイン系の技術に明るい方がおらず、自社で巻き取る形となった。旧態依然のデザインからモダンなデザインへサイトを一新させた。
コーディングについては、主要3画面&部分パーツのみの提供で、それらを依頼会社様の方で使い回して完成させる予定となっていた。
    
  - 取り組み

    依頼会社様が以前使用していたWebサイトのデザインから一新させる予定だったので、共有いただいた既存ソースは参考にならず、ほぼ0からコーディングを行った。

  - 工夫した点

    コーディング期間が3週間とタイトなスケジュールであったため、できるだけ早くアウトプットを出し、より多くのフィードバックを受け、少ない時間で品質が担保されるように工夫した。また、画面幅変更時の挙動が明確になっていない箇所が存在し、デザイナーさんと相談して技術的に可能な範囲で対応した。
作品自体は、非常に完成度が高いと同じPJに関わったデザイナーさん、デザイナー部長に評価いただけた。

## なりたいエンジニア像
組織を勝たせるエンジニアになりたいです。プロダクトがマーケットで成功したり、組織が良い状態になると、その組織に属しているより多くの人達が幸せになるからです。

## 使ってみたい技術
- Go

## 伸ばしたいスキル
- 要件定義・設計などの上流工程の開発スキル
- インフラ周りのスキル

## 言語

- 日本語
  - ネイティブ
- 英語
  - フィリピン語学学校で何とか働ける程度
  - TOEIC: 760点
