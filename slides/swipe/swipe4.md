##  アニメーション

<br>

TileLabelとGameViewControllerクラスを書き換える。

```swift
// TileLabel.swift

class TileLabel: UILabel {

    // ...

    func moveTo(pos:Point){
        let size = self.frame.size.width
        self.frame = CGRectMake( size * CGFloat(pos["x"]), size * CGFloat(pos["y"]), size, size )
    }
}


// GameViewController.swift

class GameViewController: UIViewController {

    // ...

    func updateStatus(){

        // animation
        for y in 0..board.boardSize {
            for x in 0..board.boardSize {
                let idx:Int = y * board.boardSize + x
                let text = tiles[idx].text
                if(!text || text == ""){ continue }

                let pos = board.movementBoard[y][x]
                if pos["x"] != x || pos["y"] != y {
                    self.view.bringSubviewToFront(self.tiles[idx])
                    UIView.animateWithDuration(0.2, animations:
                        { () in
                            self.tiles[idx].moveTo(pos)
                        }, completion: {(Bool) in })
                }
            }
        }

        // after 0.25 seconds
        let timer = NSTimer.scheduledTimerWithTimeInterval(0.25, target: self, selector: Selector("updateScreen:"), userInfo: nil, repeats: false)
    }

    func updateScreen(timer:NSTimer){

        // go gack tiles
        for y in 0..board.boardSize {
            for x in 0..board.boardSize {
                let idx:Int = y * board.boardSize + x
                tiles[idx].moveTo(["x":x,"y":y])
            }
        }

        // ...
    }
}
```