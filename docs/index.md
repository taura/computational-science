<link rel="stylesheet" href="scripts/style.css">

# 計算科学概論<br />田浦健次朗 {.unnumbered}

* 計算科学概論 [講義全体のホームページ](http://www.compsci-alliance.jp/)

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
* <font color=blue>2026/06/16</font> 2025年度版HP開設
* <font color=blue>2026/06/16</font> 6/22の予定
  * [説明スライド](slides/pdf/taura_lecture.pdf)
  * [計算科学概論（田浦分）の教材 (github)](https://github.com/taura/computational-science-material) を取得してください
  * 演習では, Wisteria スーパーコンピュータ (Aquarius : Intel CPU + NVIDIA GPU) を用います
  * 本格的な演習は SSH + コマンドラインで行いますが, 説明, 例題, そのコンパイルや実行のために Jupyter 環境を用います
  * [https://wisteria08.cc.u-tokyo.ac.jp:8000/jupyterhub/](https://wisteria08.cc.u-tokyo.ac.jp:8000/jupyterhub/) にアクセスして, [Wisteria 利用支援ポータル](https://wisteria-www.cc.u-tokyo.ac.jp/cgi-bin/hpcportal.ja/index.cgi) にログインするために配布されたIDなどを用いてログインしてください
* 教材の使い方は、上記 github レポジトリの [README.md](https://github.com/taura/computational-science-material/blob/main/README.md) を読んで下さい

<a name="#data_sharing"> </a>

# データ収集について

本講義では、AIチューターを備えたJupyterベースのプログラミング環境を提供しています。この環境では、以下の情報を記録しています

- コードの編集・コンパイル・実行の履歴 (`%%writefile_`, `%%bash_`, `%%bash_submit` セル)
- AIへの質問およびその回答 (`%%hey` セル)
- 出力結果およびエラーメッセージ

- これらのデータは、学生がどのように学習しているか、どこで困難に直面しているか、AIツールとどのようにやり取りしているかをより深く理解するために活用されます。
- それらを成績評価に使うことはありません。
- ただし、不正利用の確認に用いることはあります。何が不正かについては以下を参照。

# 研究利用への（任意の）許諾のお願い

さらに収集されたデータは、本人の許諾の元、以下の目的に使用される場合があります。

- 講義資料および教育方法の改善
- 学習支援ツールの開発・改善
- 学習・教育に関する研究

研究目的で利用する場合は、個人を特定できる情報を適切に削除または匿名化します。
個人を特定できる情報を公開・公表することはありません。

- 上記の研究目的での利用を許諾してもよい方はこの <a href="https://forms.cloud.microsoft/r/jfyGsyf25J">フォーム</a> から許諾の意志を送信して下さい。
- 許諾するか否かは任意です（指導方法の改善のために協力いただけることを希望します）。
- 同意しない場合でも成績評価やその他の講義上の扱いにおいて不利益を受けることはありません。

また、後から同じフォームを再送することで、同意を撤回することもできます。


# スライド・資料

* [講義スライド](slides/pdf/taura_lecture.pdf). 講義資料はUTOLにもアップする予定ですが, 確定するまではこちらで更新します

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
  
