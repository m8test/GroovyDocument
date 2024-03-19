功能:

+ 设置控制台悬浮窗口最小高度,单位px

定义:

+ [ConsoleWindowConfig](/API/Floaty/ConsoleWindowConfig/README.md) minHeight(int minHeight)

参数:

+ int minHeight - 控制台悬浮窗口最小高度,单位px

返回值:

+ [ConsoleWindowConfig](/API/Floaty/ConsoleWindowConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [ConsoleWindowConfig.minHeight()](/API/Floaty/ConsoleWindowConfig/README.md?id=minHeight)
  设置控制台悬浮窗口最小高度后显示控制台悬浮窗口.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow {
    // delegate -> ConsoleWindowConfig
    // ConsoleWindowConfig.minHeight() 用于配置控制台悬浮窗口最小高度,单位为px
    minHeight(500)
}
// 由于显示悬浮窗运行在Android主线程,所以需要睡眠一段时间
$threads.sleep(1000)
// Floaty.isConsoleWindowShowed() 用于判断控制台悬浮窗口是否显示
$assert.assertTrue($floaty.isConsoleWindowShowed(), "控制台悬浮窗口已显示")
```