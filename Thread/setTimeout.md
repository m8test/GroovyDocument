```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 获取主线程
def mainThread = $threads.mainThread()
// 获取定时器
def timer = mainThread.timer()
// 添加一个延时执行的定时任务
timer.setTimeout({ Object... params ->
    // 断言当前线程为主线程
    $assert.assertTrue($threads.currentThread() == $threads.mainThread(), "当前线程为主线程")
    // 打印参数
    params.each {
        $console.log(it)
    }
}, 1000, "参数1", "参数2", "参数3")
```