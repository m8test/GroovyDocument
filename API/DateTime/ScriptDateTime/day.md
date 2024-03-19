功能:

+ 获取日期中的日

定义:

+ int day()

参数:

+ 无

返回值:

+ int - 日期中的日

示例代码:

+ 通过 [ScriptDateTime.day()](/API/DateTime/ScriptDateTime/README.md?id=day) 获取日期中的日.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// DateTimes.create() 用于创建ScriptDateTime对象
def d = $dateTimes.create($dateTimes.timestamp())
// ScriptDateTime.day() 用于获取日期中的日
$console.log(d.day())
```