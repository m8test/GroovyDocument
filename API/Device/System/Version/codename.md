功能:

+ 当前开发代码名，或字符串“REL”（如果这是发布版本）。

定义:

+ String codename()

参数:

+ 无

返回值:

+ String - 当前开发代码名，或字符串“REL”（如果这是发布版本）

示例代码:

+ 通过 [Version.codename()](/API/Device/System/Version/README.md?id=codename)
  获取当前开发代码名，或字符串“REL”（如果这是发布版本）.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.version() 用于获取Version对象
def version = system.version()
// Version.codename() 用于获取当前开发代码名，或字符串“REL”（如果这是发布版本）
def codename = version.codename()
$console.log(codename)
```