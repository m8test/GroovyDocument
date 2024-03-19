功能:

+ 构建(build)的唯一标识码

定义:

+ String fingerprint()

参数:

+ 无

返回值:

+ String - 构建(build)的唯一标识码

示例代码:

+ 通过 [System.fingerprint()](/API/Device/System/README.md?id=fingerprint) 获取构建(build)的唯一标识码.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.fingerprint() 用于获取构建(build)的唯一标识码
def fingerprint = system.fingerprint()
$console.log(fingerprint)
```