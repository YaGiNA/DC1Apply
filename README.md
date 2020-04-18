# DC1Apply
Repository of application for DC1

以下、プロット

# 現在までの研究状況
## これまでの研究の背景(1.5p.)
- SNSの発展で情報を大量・迅速に取得できるように
- 悪意によって他人を騙すために作られたフェイクニュースが拡散されやすくなった
  - 誤った認識が広がり社会的損害が生まれることも
  - 政治的トピックのみならずCOVID-19にまつわるインフォデミックが好例
- 有識者が事実関係を調べるファクトチェックでは拡散に間に合わない
- フェイクニュースの自動検出が国内外で行われている 
- 入力はニューステキスト(自然言語)や添付メディア(画像や動画)、ユーザの反応(自然言語や拡散ネットワーク)など
- 出力は真偽が多いが発信者の意図を評価し誤報・皮肉に分類することもある

## 問題点
- 読者を騙すため巧妙なつくりをもつ
  - 単純なルールベース手法では精度が不足する
- 説明可能性に欠く
  - 真偽の明確な論拠・根拠の提示ができない
  - ニューラルネットワークモデルのブラックボックス問題の一環でもある
- ユーザの反応は拡散後しか得られない
  - 速報性がない
  - 拡散の抑制にはつながりにくい

## 解決方策
- ディープニューラルネットワーク(DNN)の活用
  - 既に先行研究で使用した例が多数
- 学習でのみユーザの反応や拡散ネットワークを活用する手法の必要性
  - 運用時は上記を生成補完した上で真偽を評価する

## 研究目的・研究方法
- フェイクニュース早期発見に向け、SNS上でニュースに寄せられたコメントを生成することが真偽分類精度向上につながることを示す
  - 学習では実際に投稿されたコメントを全て含める
  - テスト時は実際に運用したときの状況を踏まえ2件に制限する

## 特色と独創的な点
- 生成タスクを含めた分類タスクである点
- 精度を失わずに速報性をもつことができる点
- 生成されたコメントは説明可能性にも流用することも可能である点

## これまでの研究経過及び得られた結果
- データセットとしてFakeNewsNetを使用
  - 記事と真偽、Twitter上でのユーザの反応(ツイートやRT、Likeなど)
- フェイクニュースそのものを生成するモデルを拡張して実装した
  - 本文・コメント3件を1セットとして扱う
- ランダムで歯抜けにして生成学習させる
  - この段階ではまだ真偽は評価しない
- テスト時はコメント1件を抜き生成させる
  - 生成コメントを含むセットで真偽を評価する
- 同じ分類モデルで生成コメントを含めず分類した場合に比べた
  - 生成コメントを含めた方が分類精度が改善した

### 問題点
- 3件全て実際のコメントで分類するよりは成績が劣る
- 生成されたコメントの文法的なクオリティが高くない
  - 説明可能性をもたせにくい
### 先行研究との関連
- ユーザの反応を活用しつつ速報性をもたせた手法は他にもある
  - 弱教師あり学習を使用したもの
  - 説明可能性をもたせることは目指していない

## 図表
- 誤報や皮肉との違いを示した表を入れる？
- ニュースやユーザの反応がもつ要素の図


# これからの研究計画
## 研究の背景(0.5p)
### これからの研究計画の背景（概要）
- 自然言語の生成タスクは近年大きく脚光を浴びている
  - OpenAI-GPT2, BERT, フェイクニュースを生成するGrover
  - より自然かつ人間が書いたものに近い文章が作りやすくなった
### 問題点(解決すべき点)
- 生成されたコメントは分類への助けにはなったが人間への説明可能性は持たせられなかった
  - 機械の助けにはなるが人間が読んでも真偽を判断する助けにはならない
### 着想に至った経緯　
- 実際にSNS上で自動検出モデルを運用することを想定する
- フェイクニュースそのものよりユーザによって拡散されやすい指摘の方法をしなければ意味がない
- どうやって？
  - 単純な真偽のみならず、決め手や理由も併記する
  - 生成されたコメントがより人間が書いたものに近付けば、人間が真偽を判断する大きな助けになる

## 研究目的・内容(0.5p...去年より半減)
### 研究目的
- より人間が書いたものに近いコメントを生成することで、説明可能性を併せ持つフェイクニュースの早期自動検出を実現する
### 研究方法・内容
#### どのような計画？何をどこまで明らかにする？
- データセットの取得
  - これまで公開されたものは英語が大多数である
  - 更にユーザの反応も併記したものとなると数は更に絞られる
  - 必要が発生した場合は自前で記事とユーザの反応を併せ持つデータセットを取得する
- 生成・分類モデルの開発・発展
  - 実在or生成の二択を問うA/Bテストで人間を上回る程自然なコメントを生成させる
  - より自然であればあるほど分類精度も向上するのが望ましい
- 生成されたコメントから実際に運用した場合の説明可能性の付与
  - 真偽を判断する際にポジティブな影響を与えるか主観評価を受ける

#### 所属研究室との研究との関連
- 当研究室はエージェント、知的Web、ソフトウェア工学、データマイニングの4つの分野に渡っている
  - 今回扱う機械学習はデータマイニングの一環となる
- ボスから降ってきたものではなく10割自分で選定したテーマである
  - どう書く……？
#### 異なる研究機関での活動予定
- 海外大学研究室で1年間従事することを予定している
  - テーマは保持する
  - 日本より頻繁に論文が投稿されている北米ないしは欧州を予定
    - 頻繁→データを出したい
    - 2019年のGoogle Scholarの件数？

## 研究の特色・独創的な点(1p...去年より倍増)
### 先行研究との比較
#### 本研究の特色
#### 本研究の着眼点
#### 本研究の独創的な点
### 該当テーマの国内外における競争の有無・研究の潮流
### 本研究が完成したとき予想されるインパクト及び将来の見通し(産業界含め)

## 年次計画(1p.)
### 1年
### 2年
### 3年

## 人権の保護及び法令等の遵守への対応(0.5p.)

# 研究遂行能力(1p.)

# 研究者を志望する動機、目指す研究者像、自己の長所等(1p.)
## 動機
## 目指す象
## 長所
## 特に優れた学業成績
## 受賞歴
## 留学経験
## 特色ある学外活動
