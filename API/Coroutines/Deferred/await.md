功能:

+ 等待协程执行完成/失败/取消并获得返回结果,如果等待过程中出现异常或者协程被取消会将该异常(取消异常/其他异常)抛出.

定义:

+ Object await()

参数:

+ 无

返回值:

+ Object - 协程执行完成返回的对象.

示例代码:

+ 通过 [Deferred.await()](/API/Coroutines/Deferred/README.md?id=await) 等待协程执行完成/失败/取消并获得返回结果

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope()
// CoroutineScope.async() 用于启动一个子协程,可以获得协程执行的结果(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def deferred = scope.async({
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
// Deferred.await() 用于等待协程执行完成/失败/取消并获得返回结果
def result = deferred.await()
$assert.assertTrue(result == 5050, "1-100的和")
```