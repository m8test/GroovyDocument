功能1:

+ 设置屏幕亮度

定义1:

+ [Screen](/API/Device/Screen/README.md) brightness(int brightness)

参数1:

+ int brightness - 需要设置的屏幕亮度

返回值1:

+ [Screen](/API/Device/Screen/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取屏幕亮度

定义2:

+ int brightness()

参数2:

+ 无

返回值2:

+ int - 屏幕亮度

示例代码:

+ 通过 [Screen.brightness()](/API/Device/Screen/README.md?id=brightness) 设置/获取屏幕亮度

```groovy

// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.minBrightness() 用于获取屏幕最小亮度
def minBrightness = screen.minBrightness()
// Screen.brightness(int) 用于设置屏幕亮度
screen.brightness(minBrightness)
// Screen.brightness() 用于获取屏幕亮度
$assert.assertTrue(screen.brightness() == minBrightness, "屏幕亮度为${minBrightness}")
// Screen.maxBrightness() 用于获取屏幕最大亮度
def maxBrightness = screen.maxBrightness()
// Screen.brightness(int) 用于设置屏幕亮度
screen.brightness(maxBrightness)
// Screen.brightness() 用于获取屏幕亮度
$assert.assertTrue(screen.brightness() == maxBrightness, "屏幕亮度为${maxBrightness}")
```