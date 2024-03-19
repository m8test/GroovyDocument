功能:

+ 启动一个子协程,可以获得协程执行的结果(如果[CoroutineContext](/API/Coroutines/CoroutineContext/README.md)
  设置了[Job](/API/Coroutines/CoroutineContext/README.md?id=job)参数,那么就是启动一个新协程,与启动它的协程没有父子关系)

定义:

+ [Deferred](/API/Coroutines/Deferred/README.md) async(Closure context = null, String start = null,
  Closure runnable)

参数:

+ Closure context - 配置协程上下文的闭包,默认为null
    + 参数 - 无
    + delegate - [CoroutineContext](/API/Coroutines/CoroutineContext/README.md)
+ String start - 启动模式,默认为null(DEFAULT),可选值如下,推荐不设置该参数
    + DEFAULT - 立即执行协程体，随时可以取消
    + LAZY - 只有在用户需要的情况下运行
    + ATOMIC - 立即执行协程体，但在开始运行协程体之前无法取消(不推荐使用)
    + UNDISPATCHED - 立即在当前线程执行协程体，直到第一个 suspend函数调用，这里可以理解为耗时函数(不推荐使用)
+ Closure runnable - 需要协程执行的闭包
    + 参数 - 无
    + delegate - [CoroutineScope](/API/Coroutines/CoroutineScope/README.md)

返回值:

+ [Deferred](/API/Coroutines/Deferred/README.md) - 可获取协程执行结果的对象.

示例代码:

+ 通过 [CoroutineScope.async()](/API/Coroutines/CoroutineScope/README.md?id=async) 启动两个子协程并获取结果.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope()
// CoroutineScope.async() 用于启动一个子协程,可以获得协程执行的结果(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def deferred1 = scope.async({
    // delegate -> CoroutineContext
    dispatcher("IO")
}, "DEFAULT") {
    // delegate -> CoroutineScope
    // 模拟耗时任务,计算1-100的和
    def i = 0
    def sum = 0
    while (i <= 100) {
        sum += i
        i++
    }
    sum
}
// CoroutineScope.async() 用于启动一个子协程,可以获得协程执行的结果(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def deferred2 = scope.async({
    // delegate -> CoroutineContext
    dispatcher("IO")
}, "LAZY") {
    // delegate -> CoroutineScope
    // 模拟耗时任务,计算100-200的和
    def i = 100
    def sum = 0
    while (i <= 200) {
        sum += i
        i++
    }
    sum
}
// Deferred.start() 用于运行LAZY协程
deferred2.start()
// Deferred.await() 用于等待协程执行完成/失败/取消并获得返回结果
def result1 = deferred1.await()
// Deferred.await() 用于等待协程执行完成/失败/取消并获得返回结果
def result2 = deferred2.await()
$assert.assertTrue(result1 == 5050, "1-100的和")
$assert.assertTrue(result2 == 15150, "100-200的和")
```