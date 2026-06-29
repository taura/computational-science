<link rel="stylesheet" href="scripts/style.css">

# 計算科学概論<br />田浦健次朗 {.unnumbered}

* 計算科学概論 
  * [講義全体のホームページ](http://www.compsci-alliance.jp/)
  * [UTOLコースページ](https://utol.ecc.u-tokyo.ac.jp/lms/course?idnumber=2026_0352_FEN-AP4901L1_01)

# お知らせ

* 新しいものが上です.
* <font color=blue>最初の青字部分がアナウンス日</font> です．
* <font color=red>授業をしながら更新するのでしょっちゅうreloadしてください</font>．

<!--
* <font color=blue>2026/06/29</font> 田浦分課題仕様
  * 適当な難度(cs03, cs05以上)の課題を設定
  * 並列化, SIMD化などされていないベースラインコードを書くか, シンプルなものが入手可能なら入手する, AIで生成しても良い
  * その上以下のどちらかまたは両方を, 方法と測定結果とともにまとめよ.
    * CPUでの性能向上 --- SIMD化, 命令レベル並列性向上, マルチコア向上
    * GPUでの性能向上
-->	
* <font color=blue>2026/06/29</font> 
  * 教材を少々アップデートしています（主に、並列化の練習に手頃なよう、パラメータの調整をした）
	* オプション 1: git clone し直す 
		* 以前に clone したものを mv などで名前を変えて、git clone をやり直す
		* 自分で加えた変更は気にしないか手動で反映
			* 以前にclone したディレクトリで git status, git diff など
	* オプション 2: git pull
		* 自分で加えた変更とこちらで加えた変更が衝突した場合の処理ができる人はこちら
	* オプション 3: なにもしない
		* どのみち問題サイズは適宜変更すると思って気にしない
* <font color=blue>2026/06/29</font> 田浦分課題仕様
    * 教材の後半で与えた課題のうちどれか
    * もしくは自分で設定した同程度以上の題材
	* を選び、並列化（マルチコア、GPU）、高速化（SIMDやILP向上など）を行い、問題、手法、結果などをレポートする
	* 問題のパラメータや仕様も適宜アレンジしてよい（与えられたサイズのままでは短すぎて並列化の意味がない、高速化が効きにくい場合がある）
	* 単に並列化、高速化した、という結果よりもどうなることを狙って高速化し、実際に得られた結果とのギャップなどを考察することに重きを置く

* <font color=blue>2026/06/16</font> 2026年度版HP開設
  * [説明スライド](slides/pdf/taura_lecture.pdf)
  * [計算科学概論（田浦分）の教材 (github)](https://github.com/taura/computational-science-material)
  * 演習では, Wisteria スーパーコンピュータ (Aquarius : Intel CPU + NVIDIA GPU) を用います
  * 本格的な演習は SSH + コマンドラインで行いますが, 説明, 例題, そのコンパイルや実行のために Jupyter 環境を用います
* <font color=blue>2026/06/16</font> 6/22の予定
  * [説明スライド](slides/pdf/taura_lecture.pdf) はじめに
  * [計算科学概論（田浦分）の教材 (github)](https://github.com/taura/computational-science-material)を取得、演習
  * [https://wisteria08.cc.u-tokyo.ac.jp:8000/jupyterhub/](https://wisteria08.cc.u-tokyo.ac.jp:8000/jupyterhub/) にアクセス
    * [Wisteria 利用支援ポータル](https://wisteria-www.cc.u-tokyo.ac.jp/cgi-bin/hpcportal.ja/index.cgi) にログインするために配布されたIDを用いてログイン
  * 教材の使い方は、上記 github レポジトリの [README.md](https://github.com/taura/computational-science-material/blob/main/README.md)

# スライド・資料

* [講義スライド](slides/pdf/taura_lecture.pdf). 講義資料はUTOLにもアップする予定ですが, 確定するまではこちらで更新します

<a name="#data_sharing"> </a>

# データ収集について

- 本講義では、AIチューターを備えたJupyterベースのプログラミング環境を提供しています。この環境では、以下の情報を記録しています
  - コードの編集・コンパイル・実行の履歴 (`%%writefile_`, `%%bash_`, `%%bash_submit` セル)
  - AIへの質問およびその回答 (`%%hey` セル)
  - 出力結果およびエラーメッセージ
- これらのデータは、学生がどのように学習しているか、どこで困難に直面しているか、AIツールとどのようにやり取りしているかをより深く理解するために活用されます。
  - それらを成績評価に使うことはありません。
  - ただし、不正利用の確認に用いることはあります。何が不正かについては以下を参照。

# 研究利用への（任意の）許諾のお願い

- さらに, 収集されたデータは、本人の許諾の元、以下の目的に使用される場合があります。
  - 講義資料および教育方法の改善
  - 学習支援ツールの開発・改善
  - 学習・教育に関する研究
- 研究目的で利用する場合は、個人を特定できる情報を適切に削除または匿名化します。
  - 個人を特定できる情報を公開・公表することはありません。
- 上記の研究目的での利用を許諾してもよい方はこの <a href="https://forms.cloud.microsoft/r/jfyGsyf25J">フォーム</a> から許諾の意志を送信して下さい。
  - 許諾するか否かは任意です（指導方法の改善のために協力いただけることを希望します）。
  - 同意しない場合でも成績評価やその他の講義上の扱いにおいて不利益を受けることはありません。
  - また、後から同じフォームを再送することで、同意を撤回することもできます。

# AI利用方針とガイドライン

* 本講義では、専用のJupyter環境とともに、対話できるAIチューターを提供します。
* このチューターに質問したり、自分の解答へのフィードバックを求めたりすることができます。
* 「AIに何を聞いてよいか」という点で迷うかもしれません --- 特に、AIが多くの演習問題を完全に解けてしまうことを考えると。そのような疑問を持つこと自体、真剣に学ぼうとしている証です。
* 以下では、一般原則としての考え方と、本講義における具体的な方針の両面からこの問いに答えます。

## 一般ガイドライン

* **効果的に学ぶ**ために、AIを使う際は以下を推奨します：
  * _<font color="blue">答えを容易に吸収して自分のものにできる</font>_ 質問をすること
  * 答えを理解できない質問は絶対にしないこと
  * より一般的に言えば、_<font color="blue">答えを読み解いて内面化するだけで多大な労力を要するような</font>_ 質問を避けること
* 良い目安は、_<font color="blue">AIと小さなステップで対話する</font>_ ことです。各応答をその都度読んで消化しながら進める使い方。
  * 読む気のないテキストやコードの塊をコピーしていると感じたら、それは変な使い方をしているサインと感じて下さい。
* 別の言い方をすれば：
  * _<span style="color:blue">「自分が知る必要のあることを把握して、それを聞く」</span>_ のが良い
  * _<span style="color:red">「自分がやるべきことを頼む」</span>_ のはダメ
* 学習においてAIを使う<span style="color:red">最悪</span>の方法は、<span style="color:red">自分が取り組むべき課題をAIにやらせること</span>です。
  * AIの回答をそのまま提出すれば、自分で考え学ぶ力はたちまち衰えていきます。
  * たとえ回答を注意深く読んで理解しようとしても、それでも物事の仕組みを学ぶ効果的な方法とは言えません。<span style="color:red">大きなデータベースソフトのソースコードを読むのが、データベースの仕組みを効率よく学ぶ良い方法でないことと同じ</span>
* 簡単な例を挙げると、$a$、$b$、$c$ を受け取り $\cos(a + b + c)$ を計算する関数を書くよう求められたが、使用する言語をまだ知らないとします。
* このような質問をすべきです：
  * 言語Xで関数はどのように定義するか？
  * 言語Xでコサイン関数はどのように呼び出すか？
  * その他、課題を解くために必要だと思うこと
* 以下のような質問の仕方はダメ：
  * 言語Xで $a$、$b$、$c$ を受け取り $\cos(a + b + c)$ を返す関数を書いてください。
* この小さな例では違いがわかりにくいかもしれませんが、趣旨は伝わるかと思います。
* なおこれは、業務の生産性向上のために「高度な」AI活用としてよく語られるものとほぼ正反対です：
  * 業務の生産性向上を目的とする場合、人間の関与を最小限にしてAIシステムやエージェントにできるだけ多くの作業を委ねることが目標とされる。
  * その考え方が正しいかどうかはさておき、業務効率が目標であれば、作業を細かいステップに分けるより、大きく結果指向の指示を出す方が理にかなうことが多いです。
* しかし学習においては、状況は根本的に異なります：
  * 問題を小さな断片に分解し、AIとステップごとに対話することが不可欠です。なぜなら、_<font color="blue">各応答から学ぶこと自体が目的</font>_ だからです。
  * 副次的な効果として、質問を明確に言語化する力 --- _<font color="blue">自分が何を知らないかを知る力</font>_ --- も身につきます。
* 問題をどう分解すればよいかわからない場合は、その点をAIに聞いても構いません（例：<span style="color:blue">「全くわかりません。この問題にアプローチするために何を学べばよいですか？」</span>）。
* 念の為：
  * 学習にAIを使うこと自体に反対しているわけではありません（むしろうまく使うことを推奨）。
  * また、学習においては効率は重要でない（苦労が重要）、と言いたいわけでもありません。
* 要点は、_<font color="blue">効率よく学ぶ</font>_ ことと、単に _<font color="red">効率よく作業を終える</font>_ こととは根本的に異なるということです。学習とは _<span style="color:blue">脳に持続的な変化をもたらすこと</span>_ です。目的に合わせて使うことが大事です。

## 本講義における具体的な方針

* <span style="color:blue">[OK]</span> 問題を解くための一般的な質問（例：Fortranで関数を書く方法）
* <span style="color:blue">[OK]</span> 問題をステップに分解するためのヒントを求めること
* <span style="color:blue">[OK]</span> 自分の解答の誤りを指摘してもらうこと（例：エラーのデバッグ）
* <span style="color:blue">[OK]</span> 自分の解答へのフィードバックを求めること
* <span style="color:blue">[OK]</span> 講義後半の大きな問題では、明確に定義された小さなコンポーネントの生成をAIに依頼すること
* <span style="color:red">[NG]</span> 講義前半の小さな問題で、解答全体の生成をAIに依頼すること
* <span style="color:red">[NG]</span> 実質的にコードを書いてしまう自動補完ツール（例：GitHub Copilot）の使用
* <span style="color:red">[NG]</span> プロジェクトの大部分を一つのプロンプトで生成するようAIに依頼すること

* 判断が難しいケースは常に生じます。迷った場合は原則に立ち返るか、私に相談してください。

# Wisteria バッチスクリプトの設定チートシート

* 参考情報
  * Aquarius のノード : Intel CPU 72コア + 8 GPU (1 GPUあたり9コア)
  * Odyssey のノード : Fujitsu A64FX 48コア

* 推奨値
  * Aquarius用
```
#PJM -L rscgrp=lecture-a   # またはlecture9-a
#PJM -L elapse=0:01:00     # <- 左記は1分. 必要に応じて伸ばす
#PJM -L gpu=1
#PJM --omp thread=9
#PJM -g gt69
#PJM -j
#PJM -o 0output.txt
```
  * Odyssey用推奨値
```
#PJM -L rscgrp=lecture-o   # またはlecture9-o
#PJM -L elapse=0:01:00     # <- 左記は1分. 必要に応じて伸ばす
#PJM -L node=1
#PJM --omp thread=48
#PJM -g gt69
#PJM -j
#PJM -o 0output.txt
```

* よく使う設定と妥当な値
  * <font color=blue>`#PJM -L rscgrp=...`</font>
    * <font color=blue>`#PJM -L rscgrp=lecture-a`</font> : Aquarius (Intel CPU + NVIDIA GPU)
    * <font color=blue>`#PJM -L rscgrp=lecture9-a`</font> : 同上. 授業中
    * <font color=blue>`#PJM -L rscgrp=lecture-o`</font> : Odyssey (Fujitsu A64FX)
    * <font color=blue>`#PJM -L rscgrp=lecture9-o`</font> : 同上. 授業中
  * <font color=blue>`#PJM -L gpu=...`</font> : Aquarius のときに必須 (<font color=blue>1-4</font>), Odysseyでは無効
  * <font color=blue>`#PJM --omp thread=...`</font> : 使うコア数を指定するが, これは最大値にしておいて`OMP_NUM_THREADS`で調節するのが推奨
    * Aquarius : <font color=blue>1 - 「gpu= で指定した数」 x 9</font> (= 72/8). 有効な設定の例
      * <font color=blue>`#PJM -L gpu=1` `#PJM --omp thread=9`</font>
      * <font color=blue>`#PJM -L gpu=2` `#PJM --omp thread=18`</font>
      * <font color=blue>`#PJM -L gpu=3` `#PJM --omp thread=27`</font>
      * <font color=blue>`#PJM -L gpu=4` `#PJM --omp thread=36`</font>
    * Odyssey : <font color=blue>1 - 48</font>
      * <font color=blue>`#PJM --omp thread=48`</font>
  * <font color=blue>`#PJM -L node=1`</font> : Aquariusでは無効(エラー), Odysseyでは必須. この授業では1でOK
  * <font color=blue>`#PJM -L elapse=0:01:23`</font> : 制限時間. 左記は1分23秒. 本授業のキューでは15分 (<font color=blue>0:15:00</font>)まで. 可能な範囲で短い時間を指定すれば早く実行されるかもしれない
  * <font color=blue>`#PJM -g gt69`</font> : この授業では必ずこれ(`gt69`)を指定
  * <font color=blue>`#PJM -o 0output.txt`</font> : 標準入力のファイル名 (指定しないとジョブのたびに新しいファイルができて煩わしいので決めておくのを推奨)
  * <font color=blue>`#PJM -j`</font> : 標準入力と出力を1つのファイルにする (上記と同じ理由で推奨)
  
