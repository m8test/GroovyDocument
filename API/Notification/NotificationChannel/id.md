功能:

+ 设置渠道ID

定义:

+ [NotificationChannel](/API/Notification/NotificationChannel/README.md) id(String id)

参数:

+ String id - 通知渠道的id

返回值:

+ [NotificationChannel](/API/Notification/NotificationChannel/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [NotificationChannel.id()](/API/Notification/NotificationChannel/README.md?id=id) 设置渠道ID

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