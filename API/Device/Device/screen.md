功能:

+ 获取[Screen](/API/Device/Screen/README.md)对象.

定义:

+ [Screen](/API/Device/Screen/README.md) screen()

参数:

+ 无

返回值:

+ [Screen](/API/Device/Screen/README.md) - [Screen](/API/Device/Screen/README.md)对象

示例代码:

+ 通过 [Device.screen()](/API/Device/Device/README.md?id=screen)
  获取[Screen](/API/Device/Screen/README.md)对象并判断设备是否亮屏

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.isScreenOn() 用于判断当前设备是否亮屏
def isScreenOn = screen.isScreenOn()
$console.log(isScreenOn)
```