功能:

+ 最终产品的最终用户可见名称(手机型号)

定义:

+ String model()

参数:

+ 无

返回值:

+ String - 最终产品的最终用户可见名称(手机型号)

示例代码:

+ 通过 [System.model()](/API/Device/System/README.md?id=model) 获取最终产品的最终用户可见名称(手机型号).

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.model() 用于获取最终产品的最终用户可见名称(手机型号)
def model = system.model()
$console.log(model)
```