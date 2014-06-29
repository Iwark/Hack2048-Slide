##  ゲームの属性と初期化

* <y>boardSize</y>: ボードの、１行のタイルの数
* <y>rawBoard</y>: どこが何の数字かの情報を持つ２次元配列
* <y>movementBoard</y>: 数字の移動先の情報を持つ２次元配列
* <y>updateLog</y>: 今までのゲームの履歴(詳しくは後で)

```swift
// Board.swift

typealias Point = Dictionary<String, Int>
typealias Points = Array<Point>

class Board: NSObject {

    let boardSize = 4
    var rawBoard = Int[][]()  // board state
    var movementBoard = Points[]()
    var turn:Int = 0
    var updateLog = Int[][][]()  // board history

    init(){
        super.init()
        for _ in 0..boardSize {
            rawBoard += Int[](count: boardSize, repeatedValue: 0)
            movementBoard += Points(count:boardSize, repeatedValue:["x":0, "y":0])
        }
    }

    // start a new game
    func initGame(){
        for y in 0..boardSize {
            for x in 0..boardSize {
                rawBoard[y][x] = 0
            }
        }
        updateLog = Int[][][]()
        turn = 0
    }
}
```