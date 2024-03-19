功能:

+ 获取[System](/API/Device/System/README.md)对象.

定义:

+ [System](/API/Device/System/README.md) system()

参数:

+ 无

返回值:

+ [System](/API/Device/System/README.md) - [System](/API/Device/System/README.md)对象

示例代码:

+ 通过 [Device.system()](/API/Device/Device/README.md?id=system)
  获取[System](/API/Device/System/README.md)对象并获取设备品牌

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.brand() 用于获取设备品牌
def brand = system.brand()
$console.log(brand)
```