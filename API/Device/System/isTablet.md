功能:

+ 判断设备是否为平板

定义:

+ boolean isTablet()

参数:

+ 无

返回值:

+ boolean - 如果设备是平板返回true,否则返回false

示例代码:

+ 通过 [System.isTablet()](/API/Device/System/README.md?id=isTablet) 判断设备是否为平板.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.isTablet() 用于判断设备是否为平板
$console.log("设备是否为平板", system.isTablet())
```