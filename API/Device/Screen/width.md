功能:

+ 获取屏幕宽度,屏幕宽度永远大于屏幕宽度.

定义:

+ int width()

参数:

+ 无

返回值:

+ int - 屏幕宽度.

示例代码:

+ 通过 [Screen.width()](/API/Device/Screen/README.md?id=width) 获取屏幕宽度.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.width() 用于获取屏幕宽度
def width = screen.width()
$console.log(width)
```