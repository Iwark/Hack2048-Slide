##  連想配列とタプル

<br>

連想配列: 添字に数値以外が使える配列

```
  var fruit = ["apple":"good", "banana":"bad"]
  // -> fruit["apple"] = "good", fruit["banana"] = "bad"

  var seiseki = [String:Int]()
  seiseki["kokugo"] = 40
  seiseki["english"] = 80

```

<br>

タプル: 複数の値を１つの混合値として扱う

```
  var tuple = (0, 1)
  // -> tuple.0 = 0, tuple.1 = 1

  var point = (x:0, y:1)
  // -> point.x = 0, point.y = 1
```