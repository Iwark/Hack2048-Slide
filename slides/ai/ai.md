##  aiを考える

<br>

* 評価関数
  * 端っこに大きな数値があると得点が高い
  * GameOverとなった盤面の得点が最低
* Minimax法
  * 最悪の場所に2が出現したとする(min)
  * その場合の中で最高の得点を出す(max)
* Alpha-Beta法
  * Minimaxでは時間がかかりすぎる。
  * 絶対に採用されない手はそれ以上読まない。
