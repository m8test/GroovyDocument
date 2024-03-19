功能:

+ 获取[Vibrator](/API/Device/Vibrator/README.md)对象.

定义:

+ [Vibrator](/API/Device/Vibrator/README.md) vibrator()

参数:

+ 无

返回值:

+ [Vibrator](/API/Device/Vibrator/README.md) - [Vibrator](/API/Device/Vibrator/README.md)对象

示例代码:

+ 通过 [Device.vibrator()](/API/Device/Device/README.md?id=vibrator)
  获取[Vibrator](/API/Device/Vibrator/README.md)对象并震动设备

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.vibrator() 用于获取Vibrator对象
def vibrator = $device.vibrator()
// Vibrator.vibrate() 用于震动设备
vibrator.vibrate(1000)
```