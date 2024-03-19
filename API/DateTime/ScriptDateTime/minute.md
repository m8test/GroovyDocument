功能:

+ 获取日期中的分

定义:

+ int minute()

参数:

+ 无

返回值:

+ int - 日期中的分

示例代码:

+ 通过 [ScriptDateTime.minute()](/API/DateTime/ScriptDateTime/README.md?id=minute) 获取日期中的分.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// DateTimes.create() 用于创建ScriptDateTime对象
def d = $dateTimes.create($dateTimes.timestamp())
// ScriptDateTime.minute() 用于获取日期中的分
$console.log(d.minute())
```