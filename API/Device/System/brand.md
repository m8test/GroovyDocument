功能:

+ 获取设备品牌.

定义:

+ String brand()

参数:

+ 无

返回值:

+ String - 设备品牌

示例代码:

+ 通过 [System.brand()](/API/Device/System/README.md?id=brand) 获取设备品牌

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.brand() 用于获取设备品牌
def brand = system.brand()
$console.log(brand)
```