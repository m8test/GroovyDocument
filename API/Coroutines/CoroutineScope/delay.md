功能:

+ 协程延时,如果协程被取消会抛出异常(方便协程取消操作)
  ,一般情况下在协程中使用此方法代替 [Threads.sleep()](/API/Thread/Threads/README.md?id=sleep) 实现延时功能.

定义:

+ [CoroutineScope](/API/Coroutines/CoroutineScope/README.md) delay(long time)

参数:

+ long time - 延时时间,单位毫秒

返回值:

+ [CoroutineScope](/API/Coroutines/CoroutineScope/README.md) - 返回对象本身方便链式调用.

示例代码:

+ 通过 [CoroutineScope.delay()](/API/Coroutines/CoroutineScope/README.md?id=delay) 实现协程延时功能.

```groovy

// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope()
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job = scope.launch({
    // delegate -> CoroutineContext
    dispatcher("IO")
}, "DEFAULT") {
    // delegate -> CoroutineScope
    def count = 0
    while (true) {
        $console.log("子协程->$count")
        // CoroutineScope.delay() 用于协程延时
        delay(10)
        count++
    }
    // 错误示例,这会导致协程无法取消
//    while (true) {
//        $console.log("子协程->$count")
//        $threads.sleep(100)
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
    job.join()
}.catchAll {
    $console.error("job被取消:${it.message()}")
}

```