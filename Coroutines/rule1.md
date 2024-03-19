## 准则一: 协程的取消需要内部配合

### 问题: cancel() 不被响应

```groovy
// Coroutines.newScope() 用于创建一个新的协程作用域
def scope = $coroutines.newScope {
    // delegate -> CoroutineContext
    // CoroutineContext.dispatcher() 用于配置协程调度器
    dispatcher("Default")
}
// CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
def job1 = scope.launch {
    // delegate -> CoroutineScope
     
}
// Job.join() 用于等待协程执行完成
job1.join()
```