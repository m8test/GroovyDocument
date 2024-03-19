功能:

+ 添加脚本中断监听器

定义:

+ int addOnInterruptListener(Closure closure)

参数:

+ Closure closure - 设置监听器的闭包
    + 参数 - 无
    + delegate - 无

返回值:

+ int - 监听器id

示例代码:

+ 通过 [Script.addOnInterruptListener()](/API/Script/Script/README.md?id=addOnInterruptListener)
  方法添加脚本中断监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Script.addOnInterruptListener() 用于添加脚本中断监听器
$script.addOnInterruptListener {
    $console.log("script is interrupted")
}
// 获取脚本主线程
def mainThread = $threads.mainThread()
// 获取线程对应的Timer(定时器)
def timer = mainThread.timer()
// 用于记录定时任务执行的次数
def count = 1
// 定时任务id
def taskId = 0
// 设置定时任务,每隔200毫秒打印一次,打印3此后清除定时任务
taskId = timer.setInterval({
    // Script.isInterrupted() 用于判断当前脚本是否已经中断
    def isInterrupted = $script.isInterrupted()
    if (isInterrupted) {
        // 取消定时任务,如果不取消定时任务,那么主线程就不会停止.
        timer.clearInterval(taskId)
    }
    $console.log("定时任务$count")
    count++
}, 200)
// 添加一个延时执行的定时任务
timer.setTimeout({ Object... params ->
    // Script.interrupt() 用于中断脚本
    $script.interrupt()
}, 1000)
```