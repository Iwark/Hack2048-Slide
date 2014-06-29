##  ボードのスワイプ

<br>

次にボード全体のスワイプ。  
virtualがtrueの時は、実際には動かさず、  
動けたかどうかの結果だけを返す。

```swift
func swipeBoard(dir:Direction, virtual:Bool = false) -> Bool {
  var isChanged = false
  for line in 0..boardSize {
    let swipedLine:Dictionary<String, Int>[]? = self.swipeLine(line, dir:dir)

    if let l = swipedLine {
      isChanged = true
      if !virtual {
        for (idx,num) in enumerate(l) {
          switch dir {
          case .Right:
            movementBoard[line][boardSize-1-num["from"]!] = ["x":boardSize-1-num["to"]!, "y":line]
            rawBoard[line][boardSize-1-idx] = num["num"]!
          case .Left:
            movementBoard[line][num["from"]!] = ["x":num["to"]!, "y":line]
            rawBoard[line][idx] = num["num"]!
          case .Up:
            movementBoard[num["from"]!][line] = ["x":line, "y":num["to"]!]
            rawBoard[idx][line] = num["num"]!
          case .Down:
            movementBoard[boardSize-1-num["from"]!][line] = ["x":line, "y":boardSize-1-num["to"]!]
            rawBoard[boardSize-1-idx][line] = num["num"]!
          }
        }
      }
    } else if(!virtual) {
      for i in 0..boardSize {
        switch dir {
        case .Right, .Left:
          movementBoard[line][i] = ["x":i, "y":line]
        case .Up, .Down:
          movementBoard[i][line] = ["x":line, "y":i]
        }
      }
    }
  }

  if isChanged {
    if !virtual{
        updateLog += rawBoard.copy()
        ++turn
    }
    return true
  }
  else { return false }
}
```