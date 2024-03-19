功能:

+ 切换协程上下文.

定义:

+ Object withContext(Closure context, Closure runnable)

参数:

+ Closure context - 需要切换成的上下文
    + 参数 - 无
    + delegate - [CoroutineContext](/API/Coroutines/CoroutineContext/README.md)
+ Closure runnable - 需要在该上下文执行的内容,可以返回一个值作为
  [CoroutineScope.withContext()](/API/Coroutines/CoroutineScope/README.md?id=withContext)
  的返回值
    + 参数 - 无
    + delegate - [CoroutineScope](/API/Coroutines/CoroutineScope/README.md)
    + 返回值 - Object

返回值:

+ Object - runnable闭包执行返回的结果

示例代码:

+ 通过 [CoroutineScope.withContext()](/API/Coroutines/CoroutineScope/README.md?id=withContext)
  切换协程上下文.

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
    // CoroutineScope.withContext() 用于切换协程上下文
    def result = withContext({
        // delegate -> CoroutineContext
        // CoroutineContext.dispatcher() 用于配置协程调度器
        dispatcher("Main")
    }) {
        // delegate -> CoroutineScope
        $console.log("更新UI", $threads.currentThread().name())
        // 这里返回true模拟成功更新UI
        true
    }
    $console.log("主线程更新UI结果:$result", $threads.currentThread().name())
}
// Job.join() 用于等待协程执行完成
job.join()
```