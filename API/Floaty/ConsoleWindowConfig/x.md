功能:

+ 设置控制台悬浮窗口x坐标,默认为0,单位px

定义:

+ [ConsoleWindowConfig](/API/Floaty/ConsoleWindowConfig/README.md) x(int x)

参数:

+ int x - 控制台悬浮窗口x坐标,单位px

返回值:

+ [ConsoleWindowConfig](/API/Floaty/ConsoleWindowConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [ConsoleWindowConfig.x()](/API/Floaty/ConsoleWindowConfig/README.md?id=x)
  设置控制台悬浮窗口x坐标后显示控制台悬浮窗口.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow {
    // delegate -> ConsoleWindowConfig
    // ConsoleWindowConfig.x() 用于配置控制台悬浮窗口x坐标,单位为px
    x(100)
}
// 由于显示悬浮窗运行在Android主线程,所以需要睡眠一段时间
$threads.sleep(1000)
// Floaty.isConsoleWindowShowed() 用于判断控制台悬浮窗口是否显示
$assert.assertTrue($floaty.isConsoleWindowShowed(), "控制台悬浮窗口已显示")
```