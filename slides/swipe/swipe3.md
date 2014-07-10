##  動作の取得と画面の更新

<br>

スワイプジェスチャーを取得し、画面を更新する。  

```swift
// GameViewController.swift

class GameViewController: UIViewController {

    // ...

    override func viewDidLoad() {
        super.viewDidLoad()

        // スワイプジェスチャーの追加
        let dirs:UISwipeGestureRecognizerDirection[] = [.Right, .Left, .Up, .Down]
        for dir in dirs{
            let sgr = UISwipeGestureRecognizer(target: self, action: Selector("swiped:"))
            sgr.direction = dir
            self.view.addGestureRecognizer(sgr)
        }
    }

    // ...

    func swiped(sender: UISwipeGestureRecognizer){
        let swipableDirections = board.swipableDirections()

        var isSwiped = false
        for dir in swipableDirections{
            if dir.swipeDir() == sender.direction.value{
                isSwiped = true
                board.swipeBoard(dir)
                break
            }
        }

        if isSwiped {
            self.updateScreen()
        }
    }

    func updateScreen(timer:NSTimer){
        for y in 0..<BOARD_SIZE {
            for x in 0..<BOARD_SIZE {
                let idx:Int = y * BOARD_SIZE + x
                let num:Int = board.rawBoard[y][x]
                tiles[idx].setNumber(num)
            }
        }

        let generatedPos = board.generateNumber()
        tiles[generatedPos].setNumber(2)
    }
}
```