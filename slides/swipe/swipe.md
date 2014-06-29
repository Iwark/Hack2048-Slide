##  スワイプメソッド

<br>

まずは１行の場合。返り値は、Optionalというやつ。  
fromとtoがあるのは、アニメーションのため。  

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

func swipeLine(line:Int, dir:Direction) -> Dictionary<String, Int>[]? {
        
    var isChanged = false
    
    var numbers = Dictionary<String, Int>[]()
    for i in 0..boardSize {
        switch dir {
        case .Right:
            numbers += ["num":rawBoard[line][boardSize-1-i], "from":i, "to":i]
        case .Left:
            numbers += ["num":rawBoard[line][i], "from":i, "to":i]
        case .Up:
            numbers += ["num":rawBoard[i][line], "from":i, "to":i]
        case .Down:
            numbers += ["num":rawBoard[boardSize-1-i][line], "from":i, "to":i]
        }
    }
    
    var num = 0
    while num < boardSize-1 {
        if(numbers[num]["num"] == 0 && numbers[num+1]["num"] > 0){
            isChanged = true
            numbers[num+1]["to"] = num
            let tempNum = numbers[num+1]
            numbers[num+1] = numbers[num]
            numbers[num] = tempNum
            num = 0 // need?
        }else{
            ++num
        }
    }
    
    var i = 0
    while(i < numbers.count - 1){
        if(numbers[i]["num"] == numbers[i+1]["num"] && numbers[i]["num"] != 0){
            isChanged = true
            numbers[i]["num"] = numbers[i]["num"]! * 2
            numbers[i]["to"] = i
            numbers[i+1]["num"] = 0
            numbers[i+1]["to"] = i
            ++i
        }
        ++i
    }
    
    num = 0
    while num < boardSize-1 {
        if(numbers[num]["num"] == 0 && numbers[num+1]["num"] > 0){
            isChanged = true
            if(num+2 < boardSize && numbers[num+1]["to"] == numbers[num+2]["to"]){
                numbers[num+2]["to"] = num
            }
            numbers[num+1]["to"] = num
            let tempNum = numbers[num+1]
            numbers[num+1] = numbers[num]
            numbers[num] = tempNum
            num = 0
        }else{
            ++num
        }
    }
    
    if isChanged { return numbers }
    else { return nil }
    
}
```
