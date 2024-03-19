功能:

+ 获取屏幕最大亮度.

定义:

+ int maxBrightness()

参数:

+ 无

返回值:

+ int - 屏幕最大亮度

示例代码:

+ 通过 [Screen.maxBrightness()](/API/Device/Screen/README.md?id=maxBrightness) 获取屏幕最大亮度.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.maxBrightness() 用于获取屏幕最大亮度
def maxBrightness = screen.maxBrightness()
$console.log(maxBrightness)
```