功能:

+ 硬件的名称（来自内核命令行或/proc）

定义:

+ String hardware()

参数:

+ 无

返回值:

+ String - 硬件的名称（来自内核命令行或/proc）

示例代码:

+ 通过 [System.hardware()](/API/Device/System/README.md?id=hardware) 获取硬件的名称（来自内核命令行或/proc）.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.hardware() 用于获取硬件的名称（来自内核命令行或/proc）
def hardware = system.hardware()
$console.log(hardware)
```