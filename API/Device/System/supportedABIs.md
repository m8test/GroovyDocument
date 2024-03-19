功能:

+ 获取设备所有支持的ABI

定义:

+ String supportedABIs()

参数:

+ 无

返回值:

+ String - 设备MAC地址

示例代码:

+ 通过 [System.supportedABIs()](/API/Device/System/README.md?id=supportedABIs) 获取设备所有支持的ABI.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.supportedABIs() 用于获取设备所有支持的ABI
$console.log("设备所有支持的ABI", system.supportedABIs())
```