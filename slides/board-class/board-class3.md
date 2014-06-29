##  ２を出現させるメソッド

<br>
数字の無いタイルを取得して、  
そのうちの１カ所をランダムに返す。
<br>

```swift
// Board.swift

class Board: NSObject {

  //  ...
  // （省略）
  //  ...
  func getEmptyPositions() -> Int[]{
    var results = Int[]()

    for y in 0..boardSize {
        for x in 0..boardSize {
            if(rawBoard[y][x] == 0){
                results += y*boardSize + x
            }
        }
    }
    return results;
  }

  func generateNumber() -> Int{
    let empties:Int[] = self.getEmptyPositions()

    let randomNum = arc4random_uniform(UInt32(empties.count))
    let randomPos = empties[Int(randomNum)]
    let y = randomPos / boardSize
    let x = randomPos % boardSize
    rawBoard[y][x] = 2

    updateLog += rawBoard.copy()
    ++turn

    return randomPos
  }
}
```