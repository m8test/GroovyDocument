功能:

+ 添加通知移除监听器,需要读取通知权限

定义:

+ boolean addOnNotificationRemovedListener(Closure closure)

参数:

+ Closure closure - 设置监听器的闭包,此闭包会在脚本主线程调用
    + 参数
        + [StatusBarNotification](https://developer.android.google.cn/reference/android/service/notification/StatusBarNotification)
          sbn - 安卓通知对象
        + [RankingMap](https://developer.android.google.cn/reference/android/service/notification/NotificationListenerService.RankingMap)
          rankingMap - 通知排名信息对象
        + int reason -
          通知被移除的原因,[https://developer.android.google.cn/reference/android/service/notification/NotificationListenerService#REASON_LISTENER_CANCEL](https://developer.android.google.cn/reference/android/service/notification/NotificationListenerService#REASON_LISTENER_CANCEL)
    + delegate - 无

返回值:

+ int - 成功时为监听器id,失败则为-1

示例代码:

+ 通过
  [Notifications.addOnNotificationRemovedListener()](/API/Notification/Notifications/README.md?id=addOnNotificationRemovedListener)
  添加通知移除监听器

```groovy
// Notifications.addOnNotificationRemovedListener() 用于添加通知移除监听器
def result = $notifications.addOnNotificationRemovedListener { sbn, rankingMap, reason ->
    $console.log(sbn, rankingMap, reason)
}
$console.log("监听器Id:$result")
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
    // Timer.setTimeout() 用于添加一个延时执行的定时任务
    timer.setTimeout({
        // 设置延时任务的目的是保证脚本主线程存活,不然通知监听器无法执行
    }, 1000)
}, 1000)
```