##  AIクラス

アルファベータ法で実装する。  

```swift
// AlphaBetaAI.swift

class AlphaBetaAI: NSObject {

  class func swipe(board:Board){

      let swipableDirections = board.swipableDirections()

      // if gameover -> return
      if swipableDirections.count == 0 {
          return
      }

      // スワイプ可能な方角が１カ所だけなら、そちらへスワイプする
      if swipableDirections.count == 1{
          board.swipeBoard(swipableDirections[0])
          return
      }

      var maxDir = alphabeta(board, limit: 3, alpha: Int.min, beta: Int.max).1

      board.swipeBoard(maxDir)
  }

  class func alphabeta(board:Board, limit:Int, alpha:Int, beta:Int) -> (Int, Direction) {
        
      var maxDir = Direction.Right

      let swipableDirections = board.swipableDirections()
      if swipableDirections.count == 0 {
          return (Evaluator.evaluate(board), maxDir)
      }
      
      if limit == 0 { return (Evaluator.evaluate(board), maxDir) }
      
      if board.turn % 2 == 0 {
          var min = Int.max
          var newBeta = beta
          let emptyPositions = board.getEmptyPositions()
          for pos in emptyPositions {
              let y = pos / BOARD_SIZE
              let x = pos % BOARD_SIZE
              board.setNumber(x, y)
              newBeta = alphabeta(board, limit: limit-1, alpha:alpha, beta:newBeta).0
              board.rawBoard[y][x] = 0
              --board.turn
              
              if beta < newBeta {
                  newBeta = beta
              }
              if alpha >= newBeta {
                  return (alpha, maxDir)
              }
          }
          println("turn: \(board.turn), beta: \(newBeta)")
          return (newBeta, maxDir)
      } else {
          var max = Int.min
          var newAlpha = alpha
          for dir in swipableDirections {
              let rawBoard = board.rawBoard
              board.swipeBoard(dir)
              newAlpha = alphabeta(board, limit: limit-1, alpha:newAlpha, beta:beta).0
              board.rawBoard = rawBoard
              --board.turn
              
              if alpha > newAlpha {
                  newAlpha = alpha
              } else {
                  maxDir = dir
              }
              if newAlpha >= beta {
                  return (beta, maxDir)
              }
          }
          println("turn: \(board.turn), alpha: \(newAlpha)")
          return (newAlpha, maxDir)
      }
  }

}

```