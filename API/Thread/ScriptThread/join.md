功能:

+ 阻塞当前线程直到调用join的线程结束运行或者到了等待时间,当前线程在等待join方法执行完成或者在等待时间内被中断时会抛出异常.

定义:

+ [ScriptThread](/API/Thread/ScriptThread/README.md) join(long millis = 0)

参数:

+ long millis - 可选,默认为0,也就是无限等待.单位为毫秒.

返回值:

+ [ScriptThread](/API/Thread/ScriptThread/README.md) - 返回对象本身方便链式调用

示例代码:

+ 开启两个子线程,子线程2等待子线程1运行结束,主线程睡眠100毫秒后中断子线程2,然后再等待子线程2 200毫秒.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 开启一个子线程不指定线程名
def thread1 = $threads.startThread({
    // 获取当前线程
    def currentThread = $threads.currentThread()
    // 断言当前线程不是主线程
    $assert.assertTrue(currentThread != $threads.mainThread(), "当前线程不是主线程")
    // 睡眠200毫秒
    $threads.sleep(200)
    $console.log("子线程1执行完毕...")
}, "子线程1")
// 开启第2个子线程并指定线程名
def thread2 = $threads.startThread({
    def currentThread = $threads.currentThread()
    // 断言当前线程不是主线程
    $assert.assertTrue(currentThread != $threads.mainThread(), "当前线程不是主线程")
    // Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
    $exceptions.tryToRun {
        // 阻塞当前线程(子线程2),直到thread1(子线程1)结束运行,如果在等待子线程1执行的过程中当前线程被中断了就会跑异常
        thread1.join()
    }.catchAll {
        $console.log("线程join时被中断了.")
    }
    // 睡眠500毫秒
    $threads.sleep(500)
    $console.log("子线程2执行完毕...")
}, "子线程2")
// 睡眠100毫秒
$threads.sleep(100)
// 中断子线程2,由于子线程1还没有执行完成,所以子线程2的thread1.join()方法会抛出异常
thread2.interrupt()
// 阻塞当前线程(主线程)200毫秒,不管子线程2有没有结束运行都会往下执行
thread2.join(200)
// 由于子线程2至少需要500毫秒才能完成,所以会先执行下面代码子线程2才会打印`子线程2执行完毕...`
$console.log("等待子线程2 200毫秒后执行的代码...")
```