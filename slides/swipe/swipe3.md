##  動作の取得と画面の更新

<br>

スワイプジェスチャーを取得し、画面を更新する。  

```swift
// GameViewController.swift

class GameViewController: UIViewController {

    // ...

    override func viewDidLoad() {
        super.viewDidLoad()

        // add swipe gesture
        let dirs:UISwipeGestureRecognizerDirection[] = [.Right, .Left, .Up, .Down]
        for dir in dirs{
            let sgr = UISwipeGestureRecognizer(target: self, action: Selector("swiped:"))
            sgr.direction = dir
            self.view.addGestureRecognizer(sgr)
        }
    }

    // ...

    func swiped(sender: UISwipeGestureRecognizer){
        if animating { return; }
        animating = true;

        var isSwiped = false

        let dirs:Direction[] = [.Right, .Left, .Up, .Down]
        for dir in dirs{
            if dir.swipeDir() == sender.direction.value{
                isSwiped = board.swipeBoard(dir)
                break
            }
        }

        if isSwiped {
            self.updateStatus()
        } else {
            animating = false;
        }
    }

    func updateStatus(){
        // after 0.25 seconds
        let timer = NSTimer.scheduledTimerWithTimeInterval(0.25, target: self, selector: Selector("updateScreen:"), userInfo: nil, repeats: false)
    }

    func updateScreen(timer:NSTimer){
        for y in 0..board.boardSize {
            for x in 0..board.boardSize {
                let idx:Int = y * board.boardSize + x
                let num:Int = board.rawBoard[y][x]
                tiles[idx].setNumber(num)
            }
        }

        let generatedPos = board.generateNumber()
        tiles[generatedPos].setNumber(2)
        animating = false;
    }
}
```