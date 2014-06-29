##  一手戻しと敗北判定

<br>

GameOverの判定を行う。

```
// Board.swift
func undo(){
    if(turn > 0){
        rawBoard = self.updateLog[turn-2].copy()
        self.updateLog.removeAtIndex(turn-1)
        self.generateNumber()
        --turn
    }
}

func isGameOver() -> Bool{

    for y in 0..boardSize {
        for x in 0..boardSize {
            if(rawBoard[y][x] == 0){
                return false
            }
        }
    }

    for dir in [Direction.Right, Direction.Up]{
        if(swipeBoard(dir)){
            self.undo()
            return false
        }
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