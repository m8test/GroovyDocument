功能:

+ 此硬件设备上当前运行的软件的SDK版本

定义:

+ int sdkInt()

参数:

+ 无

返回值:

+ int - 此硬件设备上当前运行的软件的SDK版本

示例代码:

+ 通过 [Version.sdkInt()](/API/Device/System/Version/README.md?id=sdkInt) 获取此硬件设备上当前运行的软件的SDK版本.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.version() 用于获取Version对象
def version = system.version()
// Version.sdkInt() 用于获取此硬件设备上当前运行的软件的SDK版本
def sdkInt = version.sdkInt()
$console.log(sdkInt)
```