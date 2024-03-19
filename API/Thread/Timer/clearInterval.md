功能:

+ 取消由 [Timer.setInterval()](/API/Thread/Timer/README.md?id=setInterval) 添加的定时任务.

定义:

+ boolean clearInterval(int taskId)

方法参数:

+ int taskId - 定时任务的id,即 [Timer.setInterval()](/API/Thread/Timer/README.md?id=setInterval) 返回值.

返回值:

+ boolean
    + true - 定时任务存在(取消成功)
    + false - 定时任务不存在(取消失败)

示例代码:

+ 在主线程添加一个无限循环执行的定时任务,当任务执行3次后取消该任务.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 获取脚本主线程
def mainThread = $threads.mainThread()
// 获取线程对应的Timer(定时器)
def timer = mainThread.timer()
// 用于记录定时任务执行的次数
def count = 1
// 定时任务id
def taskId = 0
// 设置定时任务,每隔200毫秒打印一次,打印3此后清除定时任务
taskId = timer.setInterval({ params ->
    // 断言当前线程为主线程
    $assert.assertTrue($threads.currentThread() == $threads.mainThread(), "当前线程为主线程")
    // 遍历传递进来的参数
    params.each {
        // 打印参数,此处分别为字符串"参数1"和"参数2"
        $console.log("setInterval $count->$it")
    }
    if (count == 3) {
        // 取消定时任务,如果不取消定时任务,那么主线程就不会停止.
        timer.clearInterval(taskId)
    }
    count++
}, 200, "参数1", "参数2")
```