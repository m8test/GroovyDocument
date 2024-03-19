功能:

+ 添加一个无限循环执行的定时任务.

定义:

+ int setInterval(Closure closure, long interval, Object... params)

参数:

+ Closure closure - 需要执行的任务
    + 参数
        + Object... params [Timer.setInterval()](/API/Thread/Timer/README.md?id=setInterval)
          的第二个参数会传递到此处
    + delegate - 无
+ long interval - 每次执行的时间间隔,单位毫秒,也就是每隔interval毫秒执行一次closure里面的内容
+ Object... params - 定时任务执行所需要的参数,可以是任意类型任意多个(0个也可以),会直接将此参数传递到closure中.

返回值

+ int - 定时任务的唯一标识(id)
  ,可以通过此值取消定时任务,也就是将其作为参数传递给 [Timer.clearInterval()](/API/Thread/Timer/README.md?id=clearInterval) .

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