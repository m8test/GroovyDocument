功能:

+ 判断设备是否已经获得Root权限

定义:

+ boolean isRooted()

参数:

+ 无

返回值:

+ boolean - 如果设备已经获取root权限返回true,否则返回false

示例代码:

+ 通过 [System.isRooted()](/API/Device/System/README.md?id=isRooted) 判断设备是否已经获得Root权限.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.isRooted() 用于判断设备是否已经获得Root权限
$console.log("设备是否已经获得Root权限", system.isRooted())
```