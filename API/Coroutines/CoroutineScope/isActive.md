功能:

+ 判断协程是否处于活跃状态,一般用于配合协程的取消.
  使用协程执行CPU密集任务时,为了能让协程正常被取消,需要通过此方法判断当前协程是否处于活跃状态,如果不处于活跃状态应该需要停止执行任务实现协程的取消,否则一直执行CPU密集型任务会导致协程无法被取消.

定义:

+ boolean isActive()

参数:

+ 无

返回值:

+ boolean - 如果协程处于活跃状态返回true,否则返回false

示例代码:

+ 通过 [CoroutineScope.isActive()](/API/Coroutines/CoroutineScope/README.md?id=isActive) 判断协程是否处于活跃状态.

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
    // CoroutineScope.isActive() 用于判断当前协程是否处于活跃状态
    while (isActive()) {
        $console.log("子协程->$count")
        count++
    }
    // 错误示例,这会导致协程无法取消
//    while (true) {
//        $console.log("子协程->$count")
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