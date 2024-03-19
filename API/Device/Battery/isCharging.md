功能:

+ 判断设备是否正在充电.

定义:

+ boolean isCharging()

参数:

+ 无

返回值:

+ boolean - 如果设备正在充电返回true,否则返回false

示例代码:

+ 通过 [Battery.isCharging()](/API/Device/Battery/README.md?id=isCharging) 判断设备是否正在充电.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.battery() 用于获取Battery对象
def battery = $device.battery()
// Battery.isCharging() 用于判断当前设备是否正在充电.
def isCharging = battery.isCharging()
$console.log(isCharging)
```