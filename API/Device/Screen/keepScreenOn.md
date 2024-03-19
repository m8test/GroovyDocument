功能:

+ 保持屏幕常亮。
    + 此函数无法阻止用户使用锁屏键等正常关闭屏幕，只能使得设备在无人操作的情况下保持屏幕常亮；同时，如果此函数调用时屏幕没有点亮，则会唤醒屏幕。
    + 在某些设备上，如果不加参数time只能在本应用界面保持屏幕常亮，在其他界面会自动失效，这是因为设备的省电策略造成的。因此，建议使用比较长的时长来代替"一直保持屏幕常亮"的功能，例如
      [Screen.keepScreenOn(3600 * 1000)](/API/Device/Screen/README.md?id=keepScreenOn) 。可以使用
      [Screen.cancelKeepingAwake()](/API/Device/Screen/README.md?id=cancelKeepingAwake) 来取消屏幕常亮。

定义:

+ Screen keepScreenOn(long time)

参数:

+ long time - 屏幕保持常亮的时间, 单位毫秒。如果不加此参数，则一直保持屏幕常亮。

返回值:

+ Screen - 返回对象本身方便链式调用

示例代码:

+ 通过 [Screen.keepScreenOn()](/API/Device/Screen/README.md?id=keepScreenOn) 保持屏幕常亮.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.keepScreenOn() 用于保持屏幕常亮
screen.keepScreenOn()
```