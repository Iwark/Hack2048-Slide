##  タイルの表示②

(とりあえず)タイルの数は 4 × 4 = 16 とする。  
以下のようにクラスを書き換え、実行して確認してみる。

```swift
// GameViewController.swift

class GameViewController: UIViewController {

    @IBOutlet var boardView: UIView

    override func viewDidLoad() {
        super.viewDidLoad()
    }
    
    override func viewDidLayoutSubviews(){
        println(__FUNCTION__)
        for y in 0..4 {
            for x in 0..4 {
                let tileSize:CGFloat = boardView.frame.size.width / 4
                let tile = TileLabel(frame:CGRectMake(tileSize * CGFloat(x), tileSize * CGFloat(y), tileSize, tileSize))
                boardView.addSubview(tile)
            }
        }
    }

}
```

※ initは削除