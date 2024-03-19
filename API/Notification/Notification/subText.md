功能:

+ 设置通知附加信息,不保证它的确切显示位置

定义:

+ [Notification](/API/Notification/Notification/README.md) subText(String text)

参数:

+ String text - 通知附加信息

返回值:

+ [Notification](/API/Notification/Notification/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [Notification.subText()](/API/Notification/Notification/README.md?id=subText) 设置通知附加信息

```groovy
// Notifications.createNotification() 用于创建通知
def notification = $notifications.createNotification {
    // delegate -> Notification
    // Notification.contentText() 用于设置通知内容文字
    contentText("通知内容文字")
    // Notification.contentTitle() 用于设置通知内容标题
    contentTitle("通知内容标题")
    // Notification.subText() 用于设置通知附加信息
    subText("附加信息")
}
// Notifications.notify() 用于发送通知
$notifications.notify("tag", 1, notification)
```