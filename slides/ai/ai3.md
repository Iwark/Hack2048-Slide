##  評価関数クラス

<br>

とりあえず、端の数値の得点を高くしてみる。

```swift
// Evaluator.swift

class Evaluator: NSObject {
   
    class func evaluate(board:Board) -> Int{
        
        if board.isGameOver() {
            return -9999
        }
        
        var score = 0
        for y in 0..<BOARD_SIZE {
            for x in 0..<BOARD_SIZE {
                if x%(BOARD_SIZE-1) == 0 { score += board.rawBoard[y][x] * 2 }
                if y%(BOARD_SIZE-1) == 0 { score += board.rawBoard[y][x] * 2 }
                score -= board.rawBoard[y][x]
            }
        }
        return score
    }
    
}


```