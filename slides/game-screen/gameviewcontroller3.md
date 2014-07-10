##  タイルクラスの編集

<br>

数字を表示するタイルとなるラベルを作成する。

<br>

```swift
// TileLabel.swift

import UIKit

class TileLabel: UILabel {
    init(frame: CGRect) {
        super.init(frame: frame)
        
        self.layer.borderWidth = 1.0  // 枠線の太さ
        self.layer.borderColor = UIColor.blackColor().CGColor  // 枠線の色
        self.layer.cornerRadius = 8.0  // 角丸の大きさ
        self.layer.masksToBounds = true  // 背景色を枠線内だけにする
        self.textAlignment = .Center  // 文字の位置
        
    }
}
```