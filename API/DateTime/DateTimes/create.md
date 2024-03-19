功能:

+ 创建 [ScriptDateTime](/API/DateTime/ScriptDateTime/README.md) 对象.

定义1:

+ [ScriptDateTime](/API/DateTime/ScriptDateTime/README.md) create(long timestamp, String timeZone =
  null)

参数1:

+ long timestamp - 时间戳
+ String timeZone - 时区,E8表示东8区,W8表示西8区(E表示东,W表示西),默认为null,选择系统时区

定义2:

+ [ScriptDateTime](/API/DateTime/ScriptDateTime/README.md) create(int year, int month, int day, int
  hour = 0, int minute = 0, int second = 0, int millis = 0, String timeZone = null)

参数2:

+ int year - 年
+ int month - 月
+ int day - 日
+ int hour - 时
+ int minute - 分
+ int second - 秒
+ int millis - 毫秒
+ String timeZone - 时区,E8表示东8区,W8表示西8区(E表示东,W表示西),默认为null,选择系统时区

返回值:

+ [ScriptDateTime](/API/DateTime/ScriptDateTime/README.md) - 日期对象

示例代码:

+ 通过 [DateTimes.create()](/API/DateTime/DateTimes/README.md?id=create)
  创建 [ScriptDateTime](/API/DateTime/ScriptDateTime/README.md) 对象.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// DateTimes.create() 用于创建ScriptDateTime对象
def d1 = $dateTimes.create($dateTimes.timestamp(), "E8")
$console.log(d1)
// DateTimes.create() 用于创建ScriptDateTime对象
def d2 = $dateTimes.create(2022, 10, 30, 21, 30, 0, 0, "E8")
$console.log(d2)
```