功能:

+ 获取日期中的月

定义:

+ int month()

参数:

+ 无

返回值:

+ int - 日期中的月

示例代码:

+ 通过 [ScriptDateTime.month()](/API/DateTime/ScriptDateTime/README.md?id=month) 获取日期中的月.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// DateTimes.create() 用于创建ScriptDateTime对象
def d = $dateTimes.create($dateTimes.timestamp())
// ScriptDateTime.month() 用于获取日期中的月
$console.log(d.month())
```