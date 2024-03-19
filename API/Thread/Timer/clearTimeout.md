功能:

+ 取消由 [Timer.setTimeout()](/API/Thread/Timer/README.md?id=setTimeout) 添加的定时任务.

定义:

+ boolean clearTimeout(int id)

参数:

+ int id - 定时任务的id, [Timer.setTimeout()](/API/Thread/Timer/README.md?id=setTimeout) 的返回值.

返回值:

+ boolean
    + true - 定时任务存在(取消成功)
    + false - 定时任务不存在(取消失败)

示例代码:

+ 添加一个延时执行的定时任务将其取消.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 获取主线程
def mainThread = $threads.mainThread()
// 获取定时器
def timer = mainThread.timer()
// 添加一个延时执行的定时任务
def taskId = timer.setTimeout({ Object... params ->
    // 断言当前线程为主线程
    $assert.assertTrue($threads.currentThread() == $threads.mainThread(), "当前线程为主线程")
    // 打印参数
    params.each {
        $console.log(it)
    }
}, 1000, "参数1", "参数2", "参数3")
// 取消taskId对应的定时任务,因为任务被取消,所以不会打印任何东西
timer.clearTimeout(taskId)
```