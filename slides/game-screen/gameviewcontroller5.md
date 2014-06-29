##  タイルの表示①

まずViewControllerのライフサイクルを考える。

* <span style="color:yellow;">viewDidLoad</span>: self.viewのロードが終了
  * ここでviewを追加することが多い
* <span style="color:yellow;">viewDidLayoutSubviews</span>: subviewsの表示
  * AutoLayout後のviewをここで追加
* <span style="color:yellow;">viewDidAppear</span>: 全部表示された後

<br>

タイルを表示するのは<span style="color:yellow;">viewDidLayoutSubviews</span>