功能:

+ 保持屏幕常亮，但允许屏幕变暗来节省电量。
    + 此函数可以用于定时脚本唤醒屏幕操作，不需要用户观看屏幕，可以让屏幕变暗来节省电量。
    + 此函数无法阻止用户使用锁屏键等正常关闭屏幕，只能使得设备在无人操作的情况下保持屏幕常亮；
    + 同时，如果此函数调用时屏幕没有点亮，则会唤醒屏幕。
      可以使用 [Screen.cancelKeepingAwake()](/API/Device/Screen/README.md?id=cancelKeepingAwake)
      来取消屏幕常亮。

定义:

+ Screen keepScreenDim(long time)

参数:

+ long time - 屏幕保持常亮的时间, 单位毫秒。如果不加此参数，则一直保持屏幕常亮。

返回值:

+ Screen - 返回对象本身方便链式调用

示例代码:

+ 通过 [Screen.keepScreenDim()](/API/Device/Screen/README.md?id=keepScreenDim) 取消设备保持唤醒状态.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.screen() 用于获取Screen对象
def screen = $device.screen()
// Screen.keepScreenDim() 用于保持屏幕常亮，但允许屏幕变暗来节省电量。
screen.keepScreenDim()
```