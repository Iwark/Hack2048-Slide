##  スタートボタンのクラス②

<br>

* @IBDesignable : LiveRenderingをするクラス
  * didSetで値をセットする
* @IBInspectable : IBで値を調節できる。

<br>

```swift
// StartButton.swift

import UIKit

@IBDesignable class StartButton: UIButton {
    
    // cornerRadius
    @IBInspectable var radius:CGFloat = 20.0 { didSet {
        self.layer.cornerRadius = radius
    } }
    
}

```