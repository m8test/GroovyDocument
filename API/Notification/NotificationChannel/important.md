功能:

+ 设置渠道重要程度

定义:

+ [NotificationChannel](/API/Notification/NotificationChannel/README.md) important(String important)

参数:

+ String important - 通知渠道的重要程度,可选值有
    + UNSPECIFIED - 表示用户未表达重要性的值。 此值用于持久化首选项，不应与实际通知相关联。
    + NONE - 不重要的通知：不显示在阴影中。
    + MIN - 最低通知重要性：仅在阴影下显示，低于首屏
    + LOW - 低通知重要性：显示在阴影中，并可能显示在状态栏中，但不会引起听觉上的干扰。
    + DEFAULT - 默认通知重要性：无处不在，发出噪音，但不影响视觉。
    + HIGH - 更高的通知重要性：无处不在，发出噪音和偷看。可以使用全屏意图。
    + MAX - 未使用

返回值:

+ [NotificationChannel](/API/Notification/NotificationChannel/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [NotificationChannel.important()](/API/Notification/NotificationChannel/README.md?id=important)
  设置渠道重要程度

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