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
        for y in 0..board.boardSize {
            for x in 0..board.boardSize {
                if x%3 == 0 { score += board.rawBoard[y][x] * 2 }
                if y%3 == 0 { score += board.rawBoard[y][x] * 2 }
                score += board.rawBoard[y][x]
            }
        }
        return score
    }
    
}


```