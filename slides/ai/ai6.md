##  AIモードの追加

<br>

AIモードをtrueにしたら、プレイヤーではなく  
AIが勝手にゲームをプレイするようにする。

```swift
// GameViewController.swift

// ...

let AIMode = true

class GameViewController: UIViewController {

  // ...

  override func viewDidLayoutSubviews(){

    // ...

    if AIMode {
      AlphaBetaAI.swipe(board)
      self.updateScreen()
    }
  }

  // ...

  func updateScreen(timer:NSTimer){

    // ...

    if board.isGameOver() {
      println("GameOver")
    }else if AIMode{
      AlphaBetaAI.swipe(board)
      self.updateStatus()
    }
  }

}
```