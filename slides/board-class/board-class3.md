##  ２を出現させるメソッド

<br>
数字の無いタイルを取得して、  
そのうちの１カ所に２の数字を出現させる
<br>

```swift
// Board.swift

class Board: NSObject {

  //  ...
  // （省略）
  //  ...

  // 盤面(x, y)に２の数字を出現させる
  func setNumber(x:Int, _ y:Int) {
    rawBoard[y][x] = 2
    ++turn
  }

  // 盤面上の空いている場所を配列で取得する
  func getEmptyPositions() -> [Int]{
    var results = [Int]()
    
    for y in 0..<BOARD_SIZE {
      for x in 0..<BOARD_SIZE {
        if(rawBoard[y][x] == 0){
            results += y*BOARD_SIZE + x
        }
      }
    }
    return results;
  }
  
  // ランダムな場所に２の数字を出現させる
  func generateNumber() -> Int{
    let empties = self.getEmptyPositions()
    
    let randomNum = arc4random_uniform(UInt32(empties.count))
    let randomPos = empties[Int(randomNum)]
    let y = randomPos / BOARD_SIZE
    let x = randomPos % BOARD_SIZE
    
    self.setNumber(x, y)
    
    return randomPos
  }
}
```