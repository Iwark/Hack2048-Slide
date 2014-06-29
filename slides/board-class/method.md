##  メソッド

何らかの処理をするもの

```
// こんな形

func メソッド名(引数1, 引数2, ...) -> 返り値の型 {
  何らかの処理
}
```

```
// 例) 足し算をするメソッド addNumbers
// num1とnum2の二つの値を受け取り、num1 + num2の結果を返す。

func addNumbers(num1:Int, _ num2:Int) -> Int {
  return num1 + num2
}
```

```
// 使い方

let sum = addNumbers(3, 5) // sum = 8になる

// addNumbersの引数にある「_」を外すと…？
// -> 第二引数以降は基本的にラベルが必要だが、「_」で省略可能

let sum = addNumbers(3, num2: 5)

```