功能:

+ 获取[Memory](/API/Device/Memory/README.md)对象.

定义:

+ [Memory](/API/Device/Memory/README.md) memory()

参数:

+ 无

返回值:

+ [Memory](/API/Device/Memory/README.md) - [Memory](/API/Device/Memory/README.md)对象

示例代码:

+ 通过 [Device.memory()](/API/Device/Device/README.md?id=memory)
  获取[Memory](/API/Device/Memory/README.md)对象并获取当前可用内存

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.memory() 用于获取Memory对象
def memory = $device.memory()
// Memory.available() 用于获取当前可用内存
def available = memory.available()
$console.log(available)
```