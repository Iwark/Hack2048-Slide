##  スワイプメソッド

<br>

まずは１行の場合。

<br>

```swift
// GameViewController.swift

enum Direction {
    case Right, Left, Up, Down
    func swipeDir() -> UInt {
        switch self{
        case .Right:
            return UISwipeGestureRecognizerDirection.Right.value
        case .Left:
            return UISwipeGestureRecognizerDirection.Left.value
        case .Up:
            return UISwipeGestureRecognizerDirection.Up.value
        case .Down:
            return UISwipeGestureRecognizerDirection.Down.value
        }
    }
}

class GameViewController: UIViewController {
  // ...
}

// Board.swift

/**
* 該当する行(列)で0以外の数値を配列に取得
*/
func getLinePositiveNumbers(line:Int, dir:Direction) -> [Int] {
    
    var numbers = [Int]()
    
    for i in 0..<BOARD_SIZE {
        var num = 0
        switch dir {
        case .Right, .Left:
            num = rawBoard[line][i]
        case .Up, .Down:
            num = rawBoard[i][line]
        }
        if num > 0 {
            numbers += num
        }
    }
    
    return numbers
    
}

/**
* 1行(列)をスワイプさせる。
* ex) [0, 2, 4, 4] -> [2, 8, 0, 0] (左の場合)
*/
func swipeLine(line:Int, dir:Direction) -> [Int] {
    
    // [0, 2, 4, 4] -> [2, 4, 4]
    var numbers = getLinePositiveNumbers(line, dir: dir)

    // [2, 4, 4] -> [2, 8]
    var i = 0
    while(i < numbers.count - 1){
        if numbers[i] == numbers[i+1]{
            numbers[i] = numbers[i] * 2
            numbers.removeAtIndex(i+1)
        }
        ++i
    }
    
    // [2, 8] -> [2, 8, 0, 0]（左の場合）
    switch dir {
    case .Left, .Up:
        numbers += [Int](count: BOARD_SIZE - numbers.count, repeatedValue: 0)
    case .Right, .Down:
        numbers = [Int](count: BOARD_SIZE - numbers.count, repeatedValue: 0) + numbers
    }
    
    return numbers
    
}
```
