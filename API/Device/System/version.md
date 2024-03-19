功能:

+ 获取[Version](/API/Device/System/Version/README.md)对象

定义:

+ [Version](/API/Device/System/Version/README.md) version()

参数:

+ 无

返回值:

+ [Version](/API/Device/System/Version/README.md) - [Version](/API/Device/System/Version/README.md)
  对象

示例代码:

+ 通过 [System.version()](/API/Device/System/README.md?id=version)
  获取[Version](/API/Device/System/Version/README.md)对象并通过该对象获取安卓SDK版本.

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