功能:

+ 获取当前可用内存.

定义:

+ long available()

参数:

+ 无

返回值:

+ long - 当前可用内存

示例代码:

+ 通过 [Memory.available()](/API/Device/Memory/README.md?id=available) 获取当前可用内存.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.memory() 用于获取Memory对象
def memory = $device.memory()
// Memory.available() 用于获取当前可用内存
def available = memory.available()
$console.log(available)
```