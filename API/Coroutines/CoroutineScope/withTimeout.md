功能:

+ 在具有指定超时时间的协程内运行给定的闭包代码块，如果超过超时,则抛出异常.

定义:

+ Object withTimeout(long timeout, Closure closure = null)

参数:

+ long timeout - 超时时间,单位毫秒
+ Closure closure - 需要协程运行的代码块
    + 参数 - 无
    + delegate - [CoroutineScope](/API/Coroutines/CoroutineScope/README.md)
    + 返回值 - Object

返回值:

+ Object - closure返回值

示例代码:

+ 通过 [CoroutineScope.withTimeout()](/API/Coroutines/CoroutineScope/README.md?id=withTimeout) 运行代码块.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope {
    // delegate -> CoroutineContext
    // CoroutineContext.dispatcher() 用于配置协程调度器
    dispatcher("Default")
}

// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job1 = scope.launch {
    // delegate -> CoroutineScope
    // CoroutineScope.withTimeout() 用于在具有指定超时时间的协程内运行给定的闭包代码块
    def result = withTimeout(1000) {
        while (true) {
            // 模拟超时
            delay(100)
        }
    }
    // 此处不会被执行,因为会超时抛出异常
    $console.log("子协程1运行结果:$result")
}

// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job2 = scope.launch {
    // delegate -> CoroutineScope
    // CoroutineScope.withTimeout() 用于在具有指定超时时间的协程内运行给定的闭包代码块
    def result = withTimeout(1000) {
        // 直接返回结果,没有超时
        1000
    }
    // 在规定时间内完成任务,所以下面代码可以执行
    $console.log("子协程2运行结果:$result")
}

// Job.join() 用于等待协程执行完成
job1.join()
// Job.join() 用于等待协程执行完成
job2.join()
```