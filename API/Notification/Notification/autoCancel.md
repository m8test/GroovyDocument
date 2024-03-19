功能:

+ 设置用户在面板中单击通知时是否自动取消该通知。

定义:

+ [Notification](/API/Notification/Notification/README.md) autoCancel(boolean value)

参数:

+ boolean value - true表示用于点击通知后自动取消,false表示用于点击通知后不自动取消

返回值:

+ [Notification](/API/Notification/Notification/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [Notification.autoCancel()](/API/Notification/Notification/README.md?id=autoCancel)
  设置用户在面板中单击通知时是否自动取消该通知

```groovy
// Notifications.createNotification() 用于设置用户在面板中单击通知时是否自动取消该通知
def notification = $notifications.createNotification {
    // delegate -> Notification
    // Notification.contentText() 用于设置通知内容文字
    contentText("通知内容文字")
    // Notification.contentTitle() 用于设置通知内容标题
    contentTitle("通知内容标题")
    // Notification.autoCancel() 用于设置用户在面板中单击通知时是否自动取消该通知
    autoCancel(true)
}
// Notifications.notify() 用于发送通知
$notifications.notify("tag", 1, notification)
```