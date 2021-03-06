# KWStepper

[![Version](https://img.shields.io/cocoapods/v/KWStepper.svg?style=flat)](http://cocoapods.org/?q=kwstepper)
[![License](https://img.shields.io/cocoapods/l/KWStepper.svg?style=flat)](https://raw.githubusercontent.com/kyleweiner/KWStepper/master/LICENSE)
[![Platform](https://img.shields.io/cocoapods/p/KWStepper.svg?style=flat)](http://cocoapods.org/?q=kwstepper)

KWStepper is a stepper control written in Swift. Unlike [UIStepper](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIStepper_Class/index.html), KWStepper allows for a fully customized UI and provides callbacks for tailoring the UX.

![KWStepper Screenshot](screenshots.png)

 KWStepper was initially created in Objective-C for [Addo Label's](http://addolabel.com/) [Counters•](https://itunes.apple.com/app/id722416562?mt=8) and is now available in Swift for you to enjoy :)

## Features

* Allows for a fully customized UI.
* Provides properties for setting different decrement and increment steps.
* Offers optional callbacks for responding to control events and tailoring the UX.

## Installation

Simply copy the files in the `KWStepper` directory into your project.

## Usage

Try the demo!

```swift
var stepper: KWStepper!

@IBOutlet weak var countLabel: UILabel!
@IBOutlet weak var decrementButton: UIButton!
@IBOutlet weak var incrementButton: UIButton!
```

```swift
stepper = KWStepper(
    decrementButton: decrementButton,
    incrementButton: incrementButton)
```

Respond to control events using the `valueChangedCallback` property.

```swift
stepper.valueChangedCallback = {
    self.countLabel.text = NSString(format: "%.f", self.stepper.value)
}
```

Or, use the target-action pattern.

```swift
stepper.addTarget(self,
    action: "stepperDidChange",
    forControlEvents: .ValueChanged)
```

```swift
func stepperDidChange() {
    countLabel.text = NSString(format: "%.f", stepper.value)
}
```

### Configuring KWStepper

With the exception of the `continuous` property, KWStepper offers everything provided by [UIStepper](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIStepper_Class/index.html) and more.

```swift
stepper.autoRepeat = true
stepper.autoRepeatInterval = 0.10
stepper.wraps = true
stepper.minimumValue = 0
stepper.maximumValue = 8
stepper.value = 0
stepper.incrementStepValue = 1
stepper.decrementStepValue = 1
```

### KWStepperDelegate

Adopting `KWStepperDelegate` provides the following optional delegate methods for tailoring the UX.

* `optional func KWStepperDidDecrement()`
* `optional func KWStepperDidIncrement()`
* `optional func KWStepperMaxValueClamped()`
* `optional func KWStepperMinValueClamped()`

In the demo, `KWStepperMaxValueClamped()` and `KWStepperMinValueClamped()` are used to show a `UIAlertView` when a limit is reached and the `wraps` property is set to `false`.

In [Counters•](https://itunes.apple.com/app/id722416562?mt=8), `KWStepperDidDecrement()` and `KWStepperDidIncrement()` are used to play different sounds when decrementing and incrementing the steppers.

### Callbacks

As an alternative to the `KWStepperDelegate` protocol, KWStepper provides the following callbacks:

* `valueChangedCallback`
* `decrementCallback`
* `incrementCallback`
* `maxValueClampedCallback`
* `minValueClampedCallback`



## Author

KWStepper was written by Kyle Weiner.

## License

KWStepper is available under the MIT license. See the LICENSE file for details.
