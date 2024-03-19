功能:

+ 隐藏控制台悬浮窗口.

定义:

+ boolean hideConsoleWindow()

参数:

+ 无

返回值:

+ boolean - 如果控制台悬浮窗已显示则返回true,否则返回false

示例代码:

+ 显示控制台悬浮窗口后通过 [Floaty.hideConsoleWindow()](/API/Floaty/Floaty/README.md?id=hideConsoleWindow)
  隐藏控制台窗口.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 由于显示悬浮窗运行在Android主线程,所以需要睡眠一段时间
$threads.sleep(1000)
// Floaty.isConsoleWindowShowed() 用于判断控制台悬浮窗口是否显示
$assert.assertTrue($floaty.isConsoleWindowShowed(), "控制台悬浮窗口已显示")
// Floaty.hideConsoleWindow() 用于隐藏控制台悬浮窗口
$assert.assertTrue($floaty.hideConsoleWindow(), "隐藏控制台窗口")
```