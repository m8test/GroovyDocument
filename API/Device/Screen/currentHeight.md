功能:

+ 获取当前屏幕高度,如果是横屏高度小于宽度,反之宽度小于高度.

定义:

+ int currentHeight()

参数:

+ 无

返回值:

+ int - 当前屏幕高度.

示例代码:

+ 通过 [Screen.currentHeight()](/API/Device/Screen/README.md?id=currentHeight) 获取当前屏幕高度.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.currentHeight() 用于获取当前屏幕高度
def currentHeight = screen.currentHeight()
$console.log(currentHeight)
```