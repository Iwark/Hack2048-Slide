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
        
        self.layer.borderWidth = 1.0
        self.layer.borderColor = UIColor.blackColor().CGColor
        self.layer.cornerRadius = 8.0
        self.layer.masksToBounds = true
        self.textAlignment = .Center
        
    }
}
```