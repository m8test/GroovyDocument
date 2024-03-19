功能1:

+ 设置屏幕亮度模式.

定义1:

+ [Screen](/API/Device/Screen/README.md) brightnessMode(int brightnessMode)

参数1:

+ int brightnessMode - 0表示手动,1表示自动

返回值1:

+ [Screen](/API/Device/Screen/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取屏幕亮度模式,0表示手动,1表示自动

定义2:

+ int brightnessMode()

参数2:

+ 无

返回值2:

+ int - 屏幕亮度模式

示例代码:

+ 通过 [Screen.brightnessMode()](/API/Device/Screen/README.md?id=brightnessMode) 设置/获取屏幕亮度模式

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.brightnessMode(int) 用于设置屏幕亮度模式,此处设置为0表示手动模式
screen.brightnessMode(0)
// Screen.brightnessMode() 用于获取屏幕亮度模式
$assert.assertTrue(screen.brightnessMode() == 0, "屏幕亮度模式为手动")
// Screen.brightnessMode(int) 用于设置屏幕亮度模式,此处设置为1表示自动模式
screen.brightnessMode(1)
// Screen.brightnessMode() 用于获取屏幕亮度模式
$assert.assertTrue(screen.brightnessMode() == 1, "屏幕亮度模式为自动")
```