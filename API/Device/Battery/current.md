功能:

+ 获取设备电量.

定义:

+ int current()

参数:

+ 无

返回值:

+ int - 设备当前电量

示例代码:

+ 通过 [Battery.current()](/API/Device/Battery/README.md?id=current) 获取设备当前电量.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.battery() 用于获取Battery对象
def battery = $device.battery()
// Battery.current() 用于获取设备当前电量
def current = battery.current()
$console.log(current)
```