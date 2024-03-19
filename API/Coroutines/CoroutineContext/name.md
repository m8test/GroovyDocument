功能1:

+ 设置协程名.

定义1:

+ [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) name(String name)

参数1:

+ String name - 协程名

返回值1:

+ [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取协程名.

定义2:

+ String name()

参数2:

+ 无

返回值2:

+ String - 协程名

示例代码:

+ 通过 [CoroutineContext.name()](/API/Coroutines/CoroutineContext/README.md?id=name) 设置/获取协程名.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope {
    // delegate -> CoroutineContext
    // CoroutineContext.exceptionHandler() 用于配置协程异常处理器
    exceptionHandler { context, e ->
        // 在此处出现异常的协程已经结束了
        $console.error("自动传播异常:${context.name()},${e.message()}")
    }
    // CoroutineContext.name(String) 用于配置协程名
    name("coroutine-name")
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job = scope.launch {
    // delegate -> CoroutineScope
    // 此异常会导致CoroutineExceptionHandler被调用
    1 / 0
}
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Job.join() 用于等待协程执行完成/失败/取消
    job.join()
}.catchAll {
    // 协程执行出现异常
    $console.error("协程执行错误", it.message())
}
```