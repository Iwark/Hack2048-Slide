##  敗北判定

<br>

GameOverの判定を行う。

```
// Board.swift

/**
* ゲームオーバー判定
*/
func isGameOver() -> Bool{
    
    for y in 0..<BOARD_SIZE {
        for x in 0..<BOARD_SIZE {
            if(rawBoard[y][x] == 0){
                return false
            }
        }
    }
    
    if swipableDirections().count != 0 {
        return false
    }
    
    return true
}

// GameViewController.swift

class GameViewController: UIViewController {
    
    // ...

    func updateScreen(timer:NSTimer){
        
        // ...

        if board.isGameOver() {
            println("GameOver")
        }
    }
}

```