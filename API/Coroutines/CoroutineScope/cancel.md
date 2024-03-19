功能:

+ 取消协程(通过抛出CancellationException实现)以及其子协程,需要注意以下几点:
    + 协程的取消需要内部配合,使用
      [CoroutineScope.isActive()](/API/Coroutines/CoroutineScope/README.md?id=isActive)
      判断是否处于活动状态或者使用 [CoroutineScope.delay()](/API/Coroutines/CoroutineScope/README.md?id=delay) 代替
      [Threads.sleep()](/API/Thread/Threads/README.md?id=sleep)
    + 不要打破协程的父子结构,也就是尽量不要使用
      [CoroutineContext.job()](/API/Coroutines/CoroutineContext/README.md?id=job)
      配置 [Job](/API/Coroutines/Job/README.md) 类型,
      如果非要使用,最好只在 [Coroutines.newScope()](/API/Coroutines/Coroutines/README.md?id=newScope)
      中配置,不要在其他地方配置
    + 如果捕获 CancellationException 需要重新抛出来,否则无法实现取消功能

定义:

+ [CoroutineScope](/API/Coroutines/CoroutineScope/README.md) cancel(String message = null)

参数:

+ String message - 抛出 CancellationException 时的 message

返回值:

+ [CoroutineScope](/API/Coroutines/CoroutineScope/README.md) - 返回对象本身方便链式调用.

示例代码:

+ 通过 [CoroutineScope.cancel()](/API/Coroutines/CoroutineScope/README.md?id=cancel) 取消协程.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope()
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job1 = scope.launch({
    // delegate -> CoroutineContext
    dispatcher("IO")
}, "DEFAULT") {
    // delegate -> CoroutineScope
    def count = 0
    // CoroutineScope.isActive() 用于判断当前协程是否处于活跃状态
    while (isActive()) {
        $console.log("子协程1->$count")
        count++
    }
    // 错误示例,这会导致协程无法取消
//    while (true) {
//        $console.log("子协程1->$count")
//    }
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job2 = scope.launch({
    // delegate -> CoroutineContext
    dispatcher("IO")
}, "DEFAULT") {
    // delegate -> CoroutineScope
    def count = 0
    while (true) {
        $console.log("子协程2->$count")
        // CoroutineScope.delay() 用于协程延时
        delay(10)
        count++
    }
    // 错误示例,这会导致协程无法取消
//    while (true) {
//        $console.log("子协程2->$count")
//        $threads.sleep(100)
//    }
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job3 = scope.launch({
    // delegate -> CoroutineContext
    dispatcher("IO")
}, "DEFAULT") {
    // delegate -> CoroutineScope
    def count = 0
    while (true) {
        $console.log("子协程3->$count")
        // Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
        $exceptions.tryToRun {
            // CoroutineScope.delay() 用于协程延时
            delay(10)
        }.catchAll {
            $console.log("延时捕获到异常")
            // 捕获到异常需要抛出,否则无法跳出while循环导致无法取消线程
            $exceptions.throwException(it)
        }
        count++
    }
    // 错误示例,这会导致协程无法取消
//    while (true) {
//        $console.log("子协程2->$count")
//        // Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
//        $exceptions.tryToRun {
//            // CoroutineScope.delay() 用于协程延时
//            delay(10)
//        }.catchAll {
//            // 捕获到异常没有抛出,无法跳出while循环导致无法取消线程
//        }
//        count++
//    }
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
scope.launch {
    // CoroutineScope.delay() 用于协程延时
    delay(30)
    // CoroutineScope.cancel() 用于取消协程以及其子协程
    scope.cancel("测试取消")
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
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Job.join() 用于等待协程完成
    job3.join()
}.catchAll {
    $console.error("job3被取消:${it.message()}")
}
```