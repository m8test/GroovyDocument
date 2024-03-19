功能:

+ 获取当前时间戳.

定义:

+ long timestamp()

参数:

+ 无

返回值:

+ long - 当前时间戳.

示例代码:

+ 通过 [DateTimes.timestamp()](/API/DateTime/DateTimes/README.md?id=timestamp) 获取当前时间戳.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// DateTimes.timestamp() 用于获取当前时间戳
def timestamp = $dateTimes.timestamp()
$console.log(timestamp)
```