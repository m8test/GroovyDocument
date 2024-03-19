功能:

+ 移除通知发送监听器,需要读取通知权限

定义:

+ boolean removeOnNotificationPostedListener(int listenerId)

参数:

+ int listenerId -
  监听器id,[Notifications.addOnNotificationPostedListener()](/API/Notification/Notifications/README.md?id=addOnNotificationPostedListener)
  返回值

返回值:

+ boolean - 移除成功返回true,失败返回false

示例代码:

+ 通过
  [Notifications.removeOnNotificationPostedListener()](/API/Notification/Notifications/README.md?id=removeOnNotificationPostedListener)
  移除通知发送监听器

```groovy
// Notifications.addOnNotificationPostedListener() 用于添加通知发送监听器
def result = $notifications.addOnNotificationPostedListener { sbn, rankingMap ->
    $console.log(sbn, rankingMap)
}
$console.log("监听器Id:$result")
// Notifications.removeOnNotificationPostedListener() 用于移除通知发送监听器
result = $notifications.removeOnNotificationPostedListener(result)
$console.log("移除监听器结果:$result")
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
    // 设置延时任务的目的是保证脚本主线程存活,不然通知监听器无法执行
}, 1000)
```