功能:

+ 判断设备是否亮屏.

定义:

+ boolean isScreenOn()

参数:

+ 无

返回值:

+ boolean - 如果设备亮屏返回true,否则返回false

示例代码:

+ 通过 [Screen.isScreenOn()](/API/Device/Screen/README.md?id=isScreenOn) 判断设备是否亮屏

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.isScreenOn() 用于判断当前设备是否亮屏
def isScreenOn = screen.isScreenOn()
$console.log(isScreenOn)
```