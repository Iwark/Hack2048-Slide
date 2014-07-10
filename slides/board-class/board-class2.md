##  ゲームの属性と初期化

<br>

以下のようにBoardクラスを編集する。

<br>

```swift
// Board.swift

let BOARD_SIZE = 4  // １行(列)のタイルの数

class Board: NSObject {

    var rawBoard = [[Int]]()  // 盤面の状態
    var turn:Int = 0  // 現在のターン

    init(){
        super.init()
        for _ in 0..<BOARD_SIZE {
            // 配列の初期化
            rawBoard += [Int](count: BOARD_SIZE, repeatedValue: 0)
        }
        updateLog += rawBoard.copy()
    }
}
```