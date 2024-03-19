功能:

+ 设置通知渠道,安卓8.0以上才有作用

定义:

+ [Notification](/API/Notification/Notification/README.md) channel(Closure closure)

参数:

+ Closure closure - 设置通知渠道的闭包
    + 参数 - 无
    + delegate - [NotificationChannel](/API/Notification/NotificationChannel/README.md)

返回值:

+ [Notification](/API/Notification/Notification/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [Notification.channel()](/API/Notification/Notification/README.md?id=channel) 设置通知渠道

```groovy
// Notifications.createNotification() 用于设置通知渠道
def notification = $notifications.createNotification {
    // delegate -> Notification
    // Notification.contentText() 用于设置通知内容文字
    contentText("通知内容文字")
    // Notification.contentTitle() 用于设置通知内容标题
    contentTitle("通知内容标题")
    // Notification.channel() 用于设置通知渠道
    channel {
        // delegate -> NotificationChannel
        // NotificationChannel.id() 用于设置渠道ID
        id("NotificationChannelID")
        // NotificationChannel.name() 用于设置渠道名称
        name("NotificationChannelName")
        // NotificationChannel.important() 用于设置渠道重要程度
        important("DEFAULT")
    }
}
// Notifications.notify() 用于发送通知
$notifications.notify("tag", 1, notification)
```