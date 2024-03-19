功能:

+ 设置通知内容标题

定义:

+ [Notification](/API/Notification/Notification/README.md) contentTitle(String title)

参数:

+ String title - 通知标题

返回值:

+ [Notification](/API/Notification/Notification/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [Notification.contentTitle()](/API/Notification/Notification/README.md?id=contentTitle)
  设置通知内容标题

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