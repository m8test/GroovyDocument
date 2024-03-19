功能:

+ 指定协程调度器.协程必须运行在一个线程上,所以要指定调度器.如果创建协程时上下文没有指定调度器,子协程会继承父协程的调度器.

定义:

+ [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) dispatcher(String dispatcher)

参数:

+ String dispatcher - 可选值有 IO, Default, Main, Unconfined
    + IO - 运行于线程池,专为阻塞任务进行了优化. 默认限制可同时活跃的线程数 ≤ 64
    + Default - 运行于线程池,专为CPU密集型计算任务进行了优化. 2 ≤ 线程数 ≤ CPU数量
    + Main - 运行于主线程,在 Android 中就是 UI 线程,用来处理一些 UI 交互的轻量级任务.
    + Unconfined - 不改变线程,在启动它的线程执行,在恢复它的线程执行.

返回值:

+ [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) - 返回对象本身方便链式调用.

示例代码:

+ 通过 [CoroutineContext.dispatcher()](/API/Coroutines/CoroutineContext/README.md?id=dispatcher)
  指定协程调度器.

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
    $console.log("子协程运行", $threads.currentThread().name())
    // CoroutineScope.withContext() 用于切换协程上下文
    withContext({
        // delegate -> CoroutineContext
        // CoroutineContext.dispatcher() 用于配置协程调度器
        dispatcher("Main")
    }) {
        $console.log("这是在Android主线程运行的代码", $threads.currentThread().name())
    }
}
// Job.join() 用于等待协程执行完成
job.join()
```