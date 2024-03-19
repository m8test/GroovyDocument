功能:

+ 判断设备是否为模拟器

定义:

+ boolean isEmulator()

参数:

+ 无

返回值:

+ boolean - 如果设备是模拟器返回true,否则返回false

示例代码:

+ 通过 [System.isEmulator()](/API/Device/System/README.md?id=isEmulator) 判断设备是否为模拟器.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.isEmulator() 用于判断设备是否为模拟器
$console.log("设备是否为模拟器", system.isEmulator())
```