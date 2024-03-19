功能:

+ 取消通知.

定义:

+ [Notifications](/API/Notification/Notifications/README.md) cancel(String tag, int id)

参数:

+ String tag - 通知的标签,可以为null
+ int id - 通知的id

返回值:

+ [Notifications](/API/Notification/Notifications/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [Notifications.cancel()](/API/Notification/Notifications/README.md?id=cancel) 取消通知

```groovy
// Notifications.createNotification() 用于创建通知
def notification = $notifications.createNotification {
    // delegate -> Notification
    // Notification.contentText() 用于设置通知内容文字
    contentText("通知内容文字")
    // Notification.contentTitle() 用于设置通知内容标题
    contentTitle("通知内容标题")
}
// Notifications.notify() 用于发送通知
$notifications.notify("tag", 1, notification)
// Threads.mainThread() 用于获取脚本主线程
def mainThread = $threads.mainThread()
// ScriptThread.timer() 用于获取线程对应的定时器
def timer = mainThread.timer()
// Timer.setTimeout() 用于添加一个延时执行的定时任务
timer.setTimeout({
    // Notifications.cancel() 用于取消通知
    $notifications.cancel("tag", 1)
}, 10000)
```