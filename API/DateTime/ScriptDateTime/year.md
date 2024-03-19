功能:

+ 获取日期中的年

定义:

+ int year()

参数:

+ 无

返回值:

+ int - 日期中的年

示例代码:

+ 通过 [ScriptDateTime.year()](/API/DateTime/ScriptDateTime/README.md?id=year) 获取日期中的年.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// DateTimes.create() 用于创建ScriptDateTime对象
def d = $dateTimes.create($dateTimes.timestamp())
// ScriptDateTime.year() 用于获取日期中的年
$console.log(d.year())
```