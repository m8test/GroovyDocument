功能:

+ 获取日期中的秒

定义:

+ int second()

参数:

+ 无

返回值:

+ int - 日期中的秒

示例代码:

+ 通过 [ScriptDateTime.second()](/API/DateTime/ScriptDateTime/README.md?id=second) 获取日期中的秒.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// DateTimes.create() 用于创建ScriptDateTime对象
def d = $dateTimes.create($dateTimes.timestamp())
// ScriptDateTime.second() 用于获取日期中的秒
$console.log(d.second())
```