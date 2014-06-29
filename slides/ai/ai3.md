##  評価関数クラス

<br>

とりあえず。

```swift
// Evaluator.swift

class Evaluator: NSObject {
   
    class func ecaluate(board:Board) -> Int{
        
        if board.isGameOver() {
            return -9999
        }
        
        var score = 0
        for y in 0..board.boardSize {
            for x in 0..board.boardSize {
                if x%4 == 0 { score += board.rawBoard[y][x] * 2 }
                if y%4 == 0 { score += board.rawBoard[y][x] * 2 }
                score += board.rawBoard[y][x]
            }
        }
        return score
    }
    
}


```