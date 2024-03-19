功能:

+ 设备在工业设计中的名称

定义:

+ String device()

参数:

+ 无

返回值:

+ String - 设备在工业设计中的名称

示例代码:

+ 通过 [System.device()](/API/Device/System/README.md?id=device) 获取设备在工业设计中的名称.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.device() 用于获取设备在工业设计中的名称
def device = system.device()
$console.log(device)
```