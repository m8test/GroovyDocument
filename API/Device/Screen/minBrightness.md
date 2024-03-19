功能:

+ 获取屏幕最小亮度.

定义:

+ int minBrightness()

参数:

+ 无

返回值:

+ int - 屏幕最小亮度

示例代码:

+ 通过 [Screen.minBrightness()](/API/Device/Screen/README.md?id=minBrightness) 获取屏幕最小亮度.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.minBrightness() 用于获取屏幕最小亮度
def minBrightness = screen.minBrightness()
$console.log(minBrightness)
```