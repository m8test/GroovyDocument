功能:

+ 判断系统是否开启Adb调试

定义:

+ boolean isAdbEnabled()

参数:

+ 无

返回值:

+ boolean - 如果系统已经开启Adb调试返回true,否则返回false

示例代码:

+ 通过 [System.isAdbEnabled()](/API/Device/System/README.md?id=isAdbEnabled) 判断系统是否开启Adb调试.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.isAdbEnabled() 用于判断系统是否开启Adb调试
$console.log("系统是否开启Adb调试", system.isAdbEnabled())
```