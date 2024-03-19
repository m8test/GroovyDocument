功能:

+ 用户可见的安全修补程序级别

定义:

+ String securityPatch()

参数:

+ 无

返回值:

+ String - 用户可见的安全修补程序级别

示例代码:

+ 通过 [Version.securityPatch()](/API/Device/System/Version/README.md?id=securityPatch)
  获取用户可见的安全修补程序级别.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.version() 用于获取Version对象
def version = system.version()
// Version.securityPatch() 用于获取用户可见的安全修补程序级别
def securityPatch = version.securityPatch()
$console.log(securityPatch)
```