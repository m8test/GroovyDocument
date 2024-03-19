```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 断言当前线程不是主线程
$assert.assertTrue($threads.currentThread() == $threads.mainThread(), "断言 \$threads.currentThread() == \$threads.mainThread() 为真")
```