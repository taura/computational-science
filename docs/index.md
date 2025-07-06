<link rel="stylesheet" href="scripts/style.css">

# 計算科学概論<br />田浦健次朗 {.unnumbered}

* 計算科学概論 [講義全体のホームページ](http://www.compsci-alliance.jp/)

# お知らせ

* 新しいものが上です.
* <font color=blue>最初の青字部分がアナウンス日</font> です．
* <font color=red>授業をしながら更新するのでしょっちゅうreloadしてください</font>．

* <font color=blue>2024/07/06</font> 7/07の予定
  * OpenMP for GPU
  * SIMD
* <font color=blue>2024/07/06</font> AIチュータについて
  * JupyterノートブックからAIに質問ができる機能を入れました
    * OpenMP, C, Fortran, ... ChatGPT同様どんな質問も受け付けます
  * 前回 clone したレポジトリを更新しているので, 使いたい人は以下のようにして(前回と違う名前で) clone して, 以降の作業をそっちで行うのがもっとも無難です
  * 具体的には
```
ln -s /work/gt47/$USER ~/.notebook/lustre
cd ~/.notebook/lustre
git clone https://github.com/taura/computational-science-code.git computational-science-code-new
```
  * これまで作業をしていたレポジトリで変更を `pull` することもできますがすでに行った作業と衝突するなど色々問題がありますので以下の説明を元に自分でできるという人だけやってください
    * 自分の作業をどこかにメモ(コピペ)
    * `git checkout .  # 自分の作業を一旦破棄` 
    * `git pull        # 変更を反映` 
    * 自分の作業を再反映
* <font color=blue>2024/07/07</font> 田浦分課題仕様
  * 適当な難度(cs03, cs05以上)の課題を設定
  * 並列化, SIMD化などされていないベースラインコードを書くか, シンプルなものが入手可能なら入手する, AIで生成しても良い
  * その上以下のどちらかまたは両方を, 方法と測定結果とともにまとめよ.
    * CPUでの性能向上 --- SIMD化, 命令レベル並列性向上, マルチコア向上
    * GPUでの性能向上
* <font color=blue>2024/06/29</font> 2025年度版HP開設
* <font color=blue>2024/06/29</font> 6/30の予定
  * [説明](slides/pdf/taura_lecture.pdf)
  * 演習では, Wisteria スーパーコンピュータ (Aquarius : Intel CPU + NVIDIA GPU) を用います
  * 本格的な演習は SSH + コマンドラインで行いますが, 説明, 例題, そのコンパイルや実行のために Jupyter 環境を用います
  * [https://wisteria08.cc.u-tokyo.ac.jp:8000/jupyterhub/](https://wisteria08.cc.u-tokyo.ac.jp:8000/jupyterhub/) にアクセスして, [Wisteria 利用支援ポータル](https://wisteria-www.cc.u-tokyo.ac.jp/cgi-bin/hpcportal.ja/index.cgi) にログインするために配布されたIDなどを用いてログインしてみてください
* 配布コードを取得するために以下を SSH + コマンドライン, Jupyter terminalなどで実行してください
```
ln -s /work/gt47/$USER ~/.notebook/lustre
cd ~/.notebook/lustre
git clone https://github.com/taura/computational-science-code.git
```
* Pythonのnotebookのセルに以下を書いて実行 (SHIFT + ENTER) しても同じことができます
```
%%bash
ln -s /work/gt47/$USER ~/.notebook/lustre
cd ~/.notebook/lustre
git clone https://github.com/taura/computational-science-code.git
```

# スライド・資料

* [講義スライド](slides/pdf/taura_lecture.pdf). 講義資料はITC-LMSにもアップする予定ですが, 確定するまではこちらで更新します

# Wisteria バッチスクリプトの設定チートシート

* 参考情報
  * Aquarius のノード : Intel CPU 72コア + 8 GPU (1 GPUあたり9コア)
  * Odyssey のノード : Fujitsu A64FX 48コア

* 推奨値
  * Aquarius用
```
#PJM -L rscgrp=lecture-a   # またはlecture7-a
#PJM -L elapse=0:01:00     # 必要に応じて伸ばす
#PJM -L gpu=1
#PJM --omp thread=9
#PJM -g gt47
#PJM -j
#PJM -o 0output.txt
```
  * Odyssey用推奨値
```
#PJM -L rscgrp=lecture-o   # またはlecture7-o
#PJM -L elapse=0:01:00     # 必要に応じて伸ばす
#PJM -L node=1
#PJM --omp thread=48
#PJM -g gt47
#PJM -j
#PJM -o 0output.txt
```

* よく使う設定と妥当な値
  * <font color=blue>`#PJM -L rscgrp=...`</font>
    * <font color=blue>`#PJM -L rscgrp=lecture-a`</font> : Aquarius (Intel CPU + NVIDIA GPU)
    * <font color=blue>`#PJM -L rscgrp=lecture7-a`</font> : 同上. 授業中
    * <font color=blue>`#PJM -L rscgrp=lecture-o`</font> : Odyssey (Fujitsu A64FX)
    * <font color=blue>`#PJM -L rscgrp=lecture7-o`</font> : 同上. 授業中
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
  * <font color=blue>`#PJM -g gt47`</font> : この授業では必ずこれ(`gt47`)を指定
  * <font color=blue>`#PJM -o 0output.txt`</font> : 標準入力のファイル名 (指定しないとジョブのたびに新しいファイルができて煩わしいので決めておくのを推奨)
  * <font color=blue>`#PJM -j`</font> : 標準入力と出力を1つのファイルにする (上記と同じ理由で推奨)
  
