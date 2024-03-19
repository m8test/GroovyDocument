功能:

+ 显示控制台悬浮窗口.

定义:

+ boolean showConsoleWindow(Closure consoleWindowConfig = null)

参数:

+ Closure consoleWindowConfig - 控制台悬浮窗配置闭包
    + 参数 - 无
    + delegate - [ConsoleWindowConfig](/API/Floaty/ConsoleWindowConfig/README.md)

返回值:

+ boolean - 如果控制台悬浮窗已显示则返回false,否则返回true

示例代码:

+ 通过 [Floaty.showConsoleWindow()](/API/Floaty/Floaty/README.md?id=showConsoleWindow) 显示控制台悬浮窗口.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 由于显示悬浮窗运行在Android主线程,所以需要睡眠一段时间
$threads.sleep(1000)
// Floaty.isConsoleWindowShowed() 用于判断控制台悬浮窗口是否显示
$assert.assertTrue($floaty.isConsoleWindowShowed(), "控制台悬浮窗口已显示")
```