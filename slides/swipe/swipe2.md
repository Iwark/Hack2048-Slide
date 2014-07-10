##  ボードのスワイプ

<br>

次にボード全体のスワイプ。  
virtualがtrueの時は、実際には動かさず、結果だけを返す。  
また、スワイプ可能な方角を返すメソッドを作っておく。

```swift
/**
* 盤面全体をスワイプさせる。
* 盤面を返す
*/
func swipeBoard(dir:Direction, virtual:Bool = false) -> [[Int]] {
    
    var isChanged = false
    
    var swipedBoard = rawBoard
    
    for line in 0..<BOARD_SIZE {
        let swipedLine = self.swipeLine(line, dir:dir)
        for i in 0..<BOARD_SIZE {
            switch dir {
            case .Right, .Left:
                swipedBoard[line][i] = swipedLine[i]
            case .Up, .Down:
                swipedBoard[i][line] = swipedLine[i]
            }
        }
    }
    if !virtual{
        rawBoard = swipedBoard
        ++turn
    }

    return swipedBoard
}

/*
* スワイプ可能な方角を返す
*/
func swipableDirections() -> [Direction]{
    
    var results = [Direction]()
    for dir in [Direction.Left, Direction.Down, Direction.Right, Direction.Up]{
        let swipedBoard = swipeBoard(dir, virtual:true)
        for i in 0..<BOARD_SIZE {
            if rawBoard[i] != swipedBoard[i] {
                results += dir
                break
            }
        }
    }
    return results
}
```