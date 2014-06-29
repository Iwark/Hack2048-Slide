##  タイルに数字をセット

<br>

TileLabelクラスに、  
数字と、背景色をセットするメソッドを作る。

```swift
// TileLabel.swift

func getHue(num:Int, hue:CGFloat = 60) -> CGFloat{
    if(num < 2){ return hue }
    if(hue == 360){ return getHue(num / 2, hue: 24 ) }
    return getHue(num / 2, hue: hue + 24 )
}

func setNumber(num:Int){
    if num == 0 {
        self.text = ""
        self.backgroundColor = UIColor.clearColor()
    } else {
        self.text = String(num)
        self.backgroundColor = UIColor(hue: getHue(num)/360, saturation: 1.0, brightness: 1.0, alpha: 1.0)
    }
}
```

色相(Hue)を使い、各数値に対応する色を決めずに  
鮮やかな色をそれぞれの数値に割り当てる。  
再帰的なメソッドは、慣れていないとわかりづらいが。