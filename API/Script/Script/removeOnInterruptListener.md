功能:

+ 移除已经添加的脚本中断监听器

定义:

+ boolean removeOnInterruptListener(int listenerId)

参数:

+ int listenerId -
  待移除的监听器id,即 [Script.addOnInterruptListener()](/API/Script/Script/README.md?id=addOnInterruptListener)
  的返回值

返回值:

+ boolean - 移除成功返回true,失败返回false

示例代码:

+ 通过
  [Script.removeOnInterruptListener()](/API/Script/Script/README.md?id=removeOnInterruptListener)
  方法移除已经添加的脚本中断监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Script.addOnInterruptListener() 用于添加脚本中断监听器
def listenerId = $script.addOnInterruptListener {
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
// Script.removeOnInterruptListener() 用于移除已经添加的脚本中断监听器
def result = $script.removeOnInterruptListener(listenerId)
$assert.assertTrue(result, "移除监听器")
```