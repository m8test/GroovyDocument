功能:

+ 获取线程名.

定义:

+ String name()

参数:

+ 无

返回值:

+ String - 线程名称

示例代码:

+ 启动两个子线程打印输出线程名,其中一个不指定线程名,另外一个不指定线程名.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 开启一个子线程不指定线程名
$threads.startThread {
    // 获取当前线程对象
    def currentThread = $threads.currentThread()
    // 断言当前线程不是主线程
    $assert.assertTrue(currentThread != $threads.mainThread())
    // 打印当前脚本名字
    $console.log(currentThread.name())
}
// 开启第2个子线程并指定线程名
$threads.startThread({
    // 获取当前线程对象
    def currentThread = $threads.currentThread()
    // 断言当前线程不是主线程
    $assert.assertTrue(currentThread != $threads.mainThread())
    // 打印当前脚本名字
    $console.log(currentThread.name())
}, "自定义子线程名")
// 断言当前线程为主线程
$assert.assertTrue($threads.currentThread() == $threads.mainThread())
```