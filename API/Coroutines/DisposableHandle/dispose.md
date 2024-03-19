功能:

+ 处理相应的对象,使其符合垃圾收集的条件.重复调用此函数无效.

定义:

+ [DisposableHandle](/API/Coroutines/DisposableHandle/README.md) dispose()

参数:

+ 无

返回值:

+ [DisposableHandle](/API/Coroutines/DisposableHandle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [DisposableHandle.dispose()](/API/Coroutines/DisposableHandle/README.md?id=dispose)
  处理相应的对象,使其符合垃圾收集的条件.重复调用此函数无效.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope {
    // delegate -> CoroutineContext
    // CoroutineContext.dispatcher() 用于配置协程调度器
    dispatcher("Default")
    // CoroutineContext.job() 用于配置Job类型
    job("SupervisorJob")
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job1 = scope.launch {
    // delegate -> CoroutineScope
    while (true) {
        // CoroutineScope.delay() 用于协程延时
        delay(100)
    }
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job2 = scope.launch {
    // delegate -> CoroutineScope
    while (true) {
        // CoroutineScope.delay() 用于协程延时
        delay(100)
    }
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
scope.launch {
    // CoroutineScope.delay() 用于协程延时
    delay(500)
    // Job.cancel() 用于取消协程以及其子协程
    job1.cancel("测试取消job1")
    job2.cancel("测试取消job2")
}

static def getMessage(it) {
    def message = null
    if (it != null) {
        message = it.message()
    }
    return message
}

// Job.invokeOnCompletion() 用于添加协程执行完成/失败/取消回调
job1.invokeOnCompletion {
    $console.log("job1->isCompleted:${job1.isCompleted()},isCancelled:${job1.isCancelled()},exception:${getMessage(it)}")
}
// Job.invokeOnCompletion() 用于添加协程执行完成/失败/取消回调
def disposable = job2.invokeOnCompletion {
    // 由于此job注册的回调被取消了,所以job2结束时下面代码不会执行,可以和job1对比
    $console.log("job2->isCompleted:${job2.isCompleted()},isCancelled:${job2.isCancelled()},exception:${getMessage(it)}")
}
// DisposableHandle.dispose() 用于处理相应的对象,使其符合垃圾收集的条件.重复调用此函数无效.
disposable.dispose()
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Job.join() 用于等待协程执行完成/失败/取消
    job1.join()
}
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Job.join() 用于等待协程执行完成/失败/取消
    job2.join()
}
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Job.join() 用于等待协程执行完成/失败/取消
    job1.join()
}
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Job.join() 用于等待协程执行完成/失败/取消
    job2.join()
}
```