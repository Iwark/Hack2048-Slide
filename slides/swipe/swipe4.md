##  アニメーション

<br>

TileLabelとGameViewControllerクラスを書き換える。

```swift
// TileLabel.swift

class TileLabel: UILabel {

    // ...

    func moveTo(pos:Point){
        let size = self.frame.size.width
        self.frame = CGRectMake( size * CGFloat(pos["x"]!), size * CGFloat(pos["y"]!), size, size )
    }
}


// GameViewController.swift

class GameViewController: UIViewController {

    // ...

    func updateStatus(){

        // after 0.01 seconds
        let timer = NSTimer.scheduledTimerWithTimeInterval(0.01, target: self, selector: Selector("updateScreen:"), userInfo: nil, repeats: false)
    }

    func updateScreen(){

        // go gack tiles
        for y in 0..<BOARD_SIZE {
            for x in 0..<BOARD_SIZE {
                let idx:Int = y * BOARD_SIZE + x
                tiles[idx].moveTo(["x":x,"y":y])
            }
        }

        // ...
    }
}
```