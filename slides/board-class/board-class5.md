##  以下の変更をし、実行

- ボードのサイズを4から、BOARD_SIZEに変更
- tiles配列でタイルを管理する
- 2を生成し、タイルにセットする

```swift
// GameViewController.swift

class GameViewController: UIViewController {
  @IBOutlet var boardView: UIView
  let board = Board()
  var tiles = TileLabel[]()

  override func viewDidLoad() {
    super.viewDidLoad()
  }

  override func viewDidLayoutSubviews(){
    for y in 0..<BOARD_SIZE {
      for x in 0..<BOARD_SIZE {
        let tileSize:CGFloat = boardView.frame.size.width / CGFloat(BOARD_SIZE)
        let tile = TileLabel(frame:CGRectMake(tileSize * CGFloat(x), tileSize * CGFloat(y), tileSize, tileSize))
        boardView.addSubview(tile)
        tiles += tile
      }
    }
    let generatedPos = board.generateNumber()
    tiles[generatedPos].setNumber(2)
  }
}
```