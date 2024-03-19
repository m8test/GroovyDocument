功能:

+ 用户可见的版本字符串

定义:

+ String release()

参数:

+ 无

返回值:

+ String - 用户可见的版本字符串

示例代码:

+ 通过 [Version.release()](/API/Device/System/Version/README.md?id=release) 获取用户可见的版本字符串.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.version() 用于获取Version对象
def version = system.version()
// Version.release() 用于获取用户可见的版本字符串
def release = version.release()
$console.log(release)
```