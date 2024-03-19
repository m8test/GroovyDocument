功能:

+ 判断异常是否为取消异常(CancelledException)

定义:

+ boolean isCancellationException(Throwable e)

参数:

+ [Throwable](/API/Exception/Throwable/README.md) e - 需要判断的异常

返回值:

+ boolean - 如果是取消异常返回true,否则返回false

示例代码:

+ 通过
  [Exceptions.isCancellationException()](/API/Exception/Exceptions/README.md?id=isCancellationException)
  判断异常是否为取消异常.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope {
    // delegate -> CoroutineContext
    // CoroutineContext.job() 用于配置Job类型
    job("SupervisorJob")
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job1 = scope.launch({
    // delegate -> CoroutineContext
    dispatcher("IO")
}, "DEFAULT") {
    // delegate -> CoroutineScope
    def count = 0
    while (true) {
        $console.log("子协程1->$count")
        // Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
        $exceptions.tryToRun {
            // CoroutineScope.delay() 用于协程延时
            delay(10)
        }.catchAll {
            // Exceptions.isCancellationException() 判断异常是否为取消异常
            $assert.assertTrue($exceptions.isCancellationException(it), "取消异常")
            // Exceptions.throwException() 用于抛出异常,捕获到异常需要抛出,否则无法跳出while循环导致无法取消线程
            $exceptions.throwException(it)
        }
        count++
    }
}
def job2 = scope.launch({
    // delegate -> CoroutineContext
    dispatcher("IO")
}, "DEFAULT") {
    // delegate -> CoroutineScope
    // Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
    $exceptions.tryToRun {
        1 / 0
    }.catchAll {
        // Exceptions.isCancellationException() 判断异常是否为取消异常
        $assert.assertFalse($exceptions.isCancellationException(it), "非取消异常")
        // Exceptions.throwException() 用于抛出异常
        $exceptions.throwException(it)
    }
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
scope.launch {
    // CoroutineScope.delay() 用于协程延时
    delay(30)
    // Job.cancel() 用于取消协程以及其子协程
    job1.cancel("测试取消job1")
}
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Job.join() 用于等待协程完成
    job1.join()
}.catchAll {
    $console.error("job1被取消:${it.message()}")
}
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Job.join() 用于等待协程完成
    job2.join()
}.catchAll {
    $console.error("job2被取消:${it.message()}")
}
```