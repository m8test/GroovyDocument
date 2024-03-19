功能:

+ 线程睡眠,如果在睡眠的时间内线程被中断则会抛出异常.

定义:

+ [Threads](/API/Thread/Threads/README.md) sleep(long millis)

参数:

+ long millis - 睡眠的时间,单位毫秒

返回值:

+ [Threads](/API/Thread/Threads/README.md) - 返回对象本身方便链式调用

示例代码:

+ 开启一个子线程每隔100毫秒打印一次,总共打印5次.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 开启一个子线程不指定线程名
def childThread = $threads.startThread {
    // 获取当前线程
    def currentThread = $threads.currentThread()
    // 断言当前线程不是主线程
    $assert.assertTrue(currentThread != $threads.mainThread(), "当前线程不是主线程")
    for (i in 0..<5) {
        // 子线程睡眠100毫秒
        // Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
        $exceptions.tryToRun {
            $threads.sleep(100)
        }.catchAll {
            // 打印输出
            $console.log("子线程在睡眠时被中断.")
            // 此处可以执行任何你想要的操作
        }
        $console.log("子线程->$i")
    }
}
// 睡眠200毫秒中断子线程
$threads.sleep(200)
// 中断子线程,子线程正在sleep,所以子线程sleep()方法会抛异常
childThread.interrupt()
```