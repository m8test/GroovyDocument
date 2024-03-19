功能:

+ 基础源代码管理用来表示此生成的内部值。

定义:

+ String incremental()

参数:

+ 无

返回值:

+ String - 基础源代码管理用来表示此生成的内部值

示例代码:

+ 通过 [Version.incremental()](/API/Device/System/Version/README.md?id=incremental)
  获取基础源代码管理用来表示此生成的内部值.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.version() 用于获取Version对象
def version = system.version()
// Version.incremental() 用于获取基础源代码管理用来表示此生成的内部值
def incremental = version.incremental()
$console.log(incremental)
```