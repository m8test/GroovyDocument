功能:

+ 创建通知.

定义:

+ [Notification](/API/Notification/Notification/README.md) createNotification(Closure closure)

参数:

+ Closure closure - 设置通知的闭包
    + 参数 - 无
    + delegate - [Notification](/API/Notification/Notification/README.md)

返回值:

+ [Notification](/API/Notification/Notification/README.md) - 新创建的通知

示例代码:

+
通过 [Notifications.createNotification()](/API/Notification/Notifications/README.md?id=createNotification)
创建通知

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
```