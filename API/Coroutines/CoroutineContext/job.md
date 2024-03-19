功能:

+ 设置协程[Job](/API/Coroutines/Job/README.md)类型,设置协程[Job](/API/Coroutines/Job/README.md)
  类型后,那么启动的新协程和启动该新协程的协程会解除父子关系,也就是启动该新协程的协程被取消的话也不会导致该新协程被取消.

定义:

+ [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) job(String job)

参数:

+ String job - 可选值如下:
    + Job - 直接子协程如果存在未捕获异常,那么将会导致其父协程取消,从而导致其他兄弟协程被取消.
    + SupervisorJob - 即使直接子协程存在未捕获异常,也不会导致其父协程取消,也就是不影响其他兄弟协程的运行.

返回值:

+ [CoroutineContext](/API/Coroutines/CoroutineContext/README.md) - 返回对象本身方便链式调用.

示例代码:

+ 通过 [CoroutineContext.job()](/API/Coroutines/CoroutineContext/README.md?id=job)
  设置协程[Job](/API/Coroutines/Job/README.md)类型.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope1 = $coroutines.newScope {
    // delegate -> CoroutineContext
    // CoroutineContext.job() 用于配置Job类型
    job("SupervisorJob")
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job1 = scope1.launch {
    // delegate -> CoroutineScope
    // 协程出现异常
    1 / 0
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job2 = scope1.launch {
    // Job.join() 用于等待协程执行完成/失败/取消
    job1.join()
    // 下面代码继续被执行
    $console.log("SupervisorJob:兄弟协程还在运行")
}
// Job.join() 用于等待协程执行完成
job2.join()

// Coroutines.newScope() 用于创建一个新的协程作用域
def scope2 = $coroutines.newScope {
    // delegate -> CoroutineContext
    // CoroutineContext.job() 用于配置Job类型
    job("Job")
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job3 = scope2.launch {
    // delegate -> CoroutineScope
    // 协程出现异常
    1 / 0
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job4 = scope2.launch {
    // Job.join() 用于等待协程执行完成/失败/取消
    job3.join()
    // 下面代码不会被执行
    $console.log("Job:兄弟协程还在运行")
}
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // Job.join() 用于等待协程执行完成/失败/取消
    job4.join()
}.catchAll {
    // 协程被取消后会抛异常,所以在此可以捕获到该异常
    $console.log("Job:兄弟协程被取消了")
}
```