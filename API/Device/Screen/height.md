功能:

+ 获取屏幕高度,屏幕高度永远大于屏幕宽度.

定义:

+ int height()

参数:

+ 无

返回值:

+ int - 屏幕高度.

示例代码:

+ 通过 [Screen.height()](/API/Device/Screen/README.md?id=height) 获取屏幕高度.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.height() 用于获取屏幕高度
def height = screen.height()
$console.log(height)
```