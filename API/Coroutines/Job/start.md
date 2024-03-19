功能:

+ 启动通过LAZY模式创建的协程

定义:

+ [Job](/API/Coroutines/Job/README.md) start()

参数:

+ 无

返回值:

+ [Job](/API/Coroutines/Job/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [Job.start()](/API/Coroutines/Job/README.md?id=start) 启动通过LAZY模式创建的协程.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope()
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job = scope.launch({
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
    $assert.assertTrue(sum == 15150, "100-200的和")
}
// Job.start() 用于启动通过LAZY模式创建的协程
job.start()
// Job.join() 用于等待协程完成
job.join()
```