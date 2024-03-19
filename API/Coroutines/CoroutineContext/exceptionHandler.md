功能:

+ 处理协程未捕获的异常,仅在顶级协程上下文(没有父协程的协程的协程上下文)设置才有效.
    + 协程构建器(协程创建)有两种形式:
      自动传播异常([CoroutineScope.launch()](/API/Coroutines/CoroutineScope/README.md?id=launch))或向用户暴露异常(
      [CoroutineScope.async()](/API/Coroutines/CoroutineScope/README.md?id=async))
      。前者这类构建器([CoroutineScope.launch()](/API/Coroutines/CoroutineScope/README.md?id=launch))
      将异常视为未捕获异常,而后者([CoroutineScope.async()](/API/Coroutines/CoroutineScope/README.md?id=async))
      则依赖用户来最终消费异常,可以通过捕获 await() 方法(消费)抛出的异常.
    + CoroutineExceptionHandler
      仅在未捕获的异常([CoroutineScope.launch()](/API/Coroutines/CoroutineScope/README.md?id=launch))
      上调用,并且只有当这些构建器用于创建一个根协程时,即该协程不是另一个协程的子协程时才会被调用.
    + 因为所有子协程(在另一个 [Job](/API/Coroutines/Job/README.md) 上下文中创建的协程)
      委托它们的父协程处理它们的异常,然后它们也委托给其父协程,以此类推直到根协程.因此永远不会使用在子协程上下文中设置的 CoroutineExceptionHandler。
    + 除此之外, [CoroutineScope.async()](/API/Coroutines/CoroutineScope/README.md?id=async)
      构建器始终会捕获所有异常并将其表示在结果 [Deferred](/API/Coroutines/Deferred/README.md) 对象中,因此它的
      CoroutineExceptionHandler 也无效。
    + 需要注意的是,你无法从 CoroutineExceptionHandler 的异常中恢复.当调用处理者的时候,协程已经完成并带有相应的异常.通常,该处理器用于记录异常,显示某种错误消息.

定义:

+ [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) exceptionHandler(Closure handler)

参数:

+ Closure handler - 异常处理器
    + 参数
        + [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) context - 异常协程的协程上下文
        + [Throwable](/API/Exception/Throwable/README.md) e - 未处理的异常
    + delegate - 无

返回值:

+ [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) - 返回对象本身方便链式调用.

示例代码:

+ 通过
  [CoroutineContext.exceptionHandler()](/API/Coroutines/CoroutineContext/README.md?id=exceptionHandler)
  配置协程异常处理器.

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
    // CoroutineContext.job() 用于配置Job类型
    job("SupervisorJob")
    // CoroutineContext.name(String) 用于配置协程名
    name("coroutine-name")
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job = scope.launch {
    // delegate -> CoroutineScope
    // 此异常会导致CoroutineExceptionHandler被调用
    1 / 0
}
// CoroutineScope.async() 用于启动一个子协程,可以获得协程执行的结果(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def deferred = scope.async {
    // 此异常不会导致CoroutineExceptionHandler被调用
    $assert.assertTrue(1 == 0, "断言异常")
}
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Deferred.await() 用于等待协程执行完成并获得其执行结果
    def result = deferred.await()
    // 此处不会被执行
    $console.log(result)
}.catchAll {
    // 此处会捕获到async启动的协程中的异常
    $console.error("用户暴露异常:${it.message()}")
}
// Job.join() 用于等待协程执行完成
job.join()
```