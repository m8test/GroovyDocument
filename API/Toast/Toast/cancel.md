功能:

+ 取消显示吐司

定义:

+ [Toast](/API/Toast/Toast/README.md) cancel()

参数:

+ 无

返回值:

+ [Toast](/API/Toast/Toast/README.md) - 返回调用对象本身,方便链式调用.

实例代码:

+ 通过 [Toast.cancel()](/API/Toast/Toast/README.md?id=cancel) 取消显示吐司

```groovy
// Toast.showLong() 用于显示长吐司
$toast.showLong("long toast")
// Threads.mainThread() 用于获取脚本主线程
def mainThread = $threads.mainThread()
// ScriptThread.timer() 用于获取线程对应的定时器
def timer = mainThread.timer()
// Timer.setTimeout() 用于添加一个延时执行的定时任务
timer.setTimeout({
    // 设置延时任务的目的是保证脚本主线程存活,不然通知监听器无法执行
    // Toast.cancel() 用于取消显示吐司
    $toast.cancel()
}, 1000)
```