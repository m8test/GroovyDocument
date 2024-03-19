功能:

+ 构建产品基于的基本操作系统。

定义:

+ String baseOS()

参数:

+ 无

返回值:

+ String - 构建产品基于的基本操作系统

示例代码:

+ 通过 [Version.baseOS()](/API/Device/System/Version/README.md?id=baseOS) 获取构建产品基于的基本操作系统.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.version() 用于获取Version对象
def version = system.version()
// Version.baseOS() 用于获取构建产品基于的基本操作系统
def baseOS = version.baseOS()
$console.log(baseOS)
```