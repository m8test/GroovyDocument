功能:

+ 新建一个协程作用域([CoroutineScope](/APi/Coroutines/CoroutineScope/README.md))

定义:

+ [CoroutineScope](/APi/Coroutines/CoroutineScope/README.md) newScope(Closure closure = null)

参数:

+ Closure closure - 为协程作用域配置协程上下文([CoroutineContext](/APi/Coroutines/CoroutineContext/README.md))
  的闭包,默认为null
    + 参数 - 无
    + delegate - [CoroutineContext](/APi/Coroutines/CoroutineContext/README.md)

返回值:

+ [CoroutineScope](/APi/Coroutines/CoroutineScope/README.md) - 新创建的协程作用域对象.

示例代码:

+ 通过 [Coroutines.newScope()](/APi/Coroutines/Coroutines/README.md?id=newScope)
  新建一个协程作用域,并通过该协程作用域启动一个子协程.

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
def job = scope.launch {
    // delegate -> CoroutineScope
    $console.log("子协程运行")
}
// Job.join() 用于等待协程执行完成
job.join()
```