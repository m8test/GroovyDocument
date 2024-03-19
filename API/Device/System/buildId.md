功能:

+ 变更列表编号或类似“M4-rc20”的标签。

定义:

+ String buildId()

参数:

+ 无

返回值:

+ String - 变更列表编号

示例代码:

+ 通过 [System.buildId()](/API/Device/System/README.md?id=buildId) 获取变更列表编号

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.buildId() 用于获取变更列表编号
def buildId = system.buildId()
$console.log(buildId)
```