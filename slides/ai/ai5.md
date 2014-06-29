##  AIクラス

ここでは次の手しか考えない、弱いAIを作る。  
また、Boardクラスにスワイプ可能な方角の配列を返す、  
swipableDirectionsメソッドを追加しておく。

```swift
// Board.swift

class Board: NSObject {

  // ...

  func swipableDirections() -> Direction[]{
    var results = Direction[]()
    for dir in [Direction.Left, Direction.Down, Direction.Right, Direction.Up]{
      if swipeBoard(dir, virtual:true){
        results += dir
      }
    }
    return results
  }
}

// AlphaBetaAI.swift

class AlphaBetaAI: NSObject {

  class func swipe(board:Board){

      let swipableDirections = board.swipableDirections()

      // if gameover -> return
      if swipableDirections.count == 0 {
          return
      }

      // if able to swipe only one direction, then swipe that direction immediately.
      if swipableDirections.count == 1{
          board.swipeBoard(swipableDirections[0])
          return
      }

      var maxScore = 0
      var maxDir:Direction = .Left

      for dir in swipableDirections {
          board.swipeBoard(dir)
          let score = Evaluator.evaluate(board)
          board.undo()

          if score > maxScore { maxScore = score; maxDir = dir }
      }

      board.swipeBoard(maxDir)
  }
}

```

(発展) α-β法で、数手先まで読むようにしてみよう！