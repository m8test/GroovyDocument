功能:

+ 唤醒设备。包括唤醒设备CPU、屏幕等。可以用来点亮屏幕,如果屏幕已经点亮则不执行任何操作

定义:

+ Screen wakeUp()

参数:

+ 无

返回值:

+ Screen - 返回对象本身方便链式调用

示例代码:

+ 通过 [Screen.wakeUp()](/API/Device/Screen/README.md?id=wakeUp) 唤醒设备.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.wakeUp() 用于唤醒设备
screen.wakeUp()
```