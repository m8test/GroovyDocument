功能:

+ 整个产品的名称

定义:

+ String product()

参数:

+ 无

返回值:

+ String - 整个产品的名称

示例代码:

+ 通过 [System.product()](/API/Device/System/README.md?id=product) 获取整个产品的名称.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.product() 用于获取整个产品的名称
def product = system.product()
$console.log(product)
```