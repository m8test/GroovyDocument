功能:

+ 如果设备处于震动状态，则取消震动。

定义:

+ [Vibrator](/API/Device/Vibrator/README.md) cancel()

参数:

+ 无

返回值:

+ [Vibrator](/API/Device/Vibrator/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [Vibrator.cancel()](/API/Device/Vibrator/README.md?id=cancel) 取消震动设备

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.vibrator() 用于获取Vibrator对象
def vibrator = $device.vibrator()
// Vibrator.vibrate() 用于震动设备
vibrator.vibrate(3000)
// Threads.sleep() 用于线程休眠
$threads.sleep(1000)
// Vibrator.cancel() 用于取消设备震动
vibrator.cancel()
```