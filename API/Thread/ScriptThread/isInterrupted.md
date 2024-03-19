功能:

+ 判断线程是否中断,需要配合 [ScriptThread.interrupt()](/API/Thread/ScriptThread/README.md?id=interrupt) 使用

定义:

+ boolean isInterrupted()

参数:

+ 无

返回值:

+ boolean
    + true 线程状态不是中断状态
    + false 线程状态为中断状态

示例代码:

+ 开启一个子线程每300毫秒打印一下信息到控制台,主线程1秒钟后中断子线程的执行.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 开启一个子线程不指定线程名
def childThread = $threads.startThread {
    // 获取当前线程
    def currentThread = $threads.currentThread()
    // 断言当前线程不是主线程
    $assert.assertTrue(currentThread != $threads.mainThread(), "当前线程不是主线程")
    // 当线程没有被中断的时候输出信息到控制台
    while (!currentThread.isInterrupted()) {
        // 如果线程没有被中断可以执行下面代码
        $console.log(currentThread.name() + " 运行中...")
        // Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
        $exceptions.tryToRun {
            // 让当前线程睡眠300毫秒,如果在睡眠的过程中线程被中断则会抛出异常
            $threads.sleep(300)
        }.catchAll {
            // 如果在睡眠过程中调用了interrupt方法会抛出异常
            $console.log(currentThread.name() + " 睡眠时被中断了.")
            // 所以需要在此处重新调用interrupt方法
            currentThread.interrupt()
        }
    }
}
// 主线程睡眠1秒钟
$threads.sleep(1000)
// 中断子线程,需要配合ScriptThread.isInterrupted()使用
childThread.interrupt()
// 断言当前线程为主线程
$assert.assertTrue($threads.currentThread() == $threads.mainThread(), "当前线程为主线程")
```