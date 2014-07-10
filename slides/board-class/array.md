##  配列

<br>

配列: 複数の値

```
  var array = [10, 20, 30]
  // -> array[0] = 10, array[1] = 20, array[2] = 30

  var array2 = [Int](count:3, repeatedValue:10)
  // -> array2[0] = 10, array2[1] = 10, array2[2] = 10

  array += 40 // 要素の追加
  // -> array = [10, 20, 30, 40]

```
多次元配列: 配列の配列

```
  var arr = [[0, 1], [2, 3]]
  // -> arr[0][0] = 0, arr[0][1] = 1, arr[1][0] = 2, arr[1][1] = 3

  var arr2 = [[Int]](count:2, repeatedValue:[1, 2])
  // -> arr2[0][0] = 1, arr[0][1] = 2, arr[1][0] = 1, arr[1][1] = 2
```