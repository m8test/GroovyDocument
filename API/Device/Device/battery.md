功能:

+ 获取[Battery](/API/Device/Battery/README.md)对象.

定义:

+ [Battery](/API/Device/Battery/README.md) battery()

参数:

+ 无

返回值:

+ [Battery](/API/Device/Battery/README.md) - [Battery](/API/Device/Battery/README.md)对象

示例代码:

+ 通过 [Device.battery()](/API/Device/Device/README.md?id=battery) 获取
  [Battery](/API/Device/Battery/README.md)对象并获取当前电量.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.battery() 用于获取Battery对象
def battery = $device.battery()
// Battery.current() 用于获取设备当前电量
def current = battery.current()
$console.log(current)
```