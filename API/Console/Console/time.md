功能:

+ 启动一个计时器来跟踪某一个操作的占用时长.
+ 每一个计时器必须拥有唯一的名字,当以此计时器名字为参数调用 [Console.timeEnd()](/API/Console/Console/README.md?id=timeEnd)
  时,浏览器将以毫秒为单位,输出对应计时器所经过的时间.
+ 此方法会返回当前时间戳.

定义:

+ long time(String timerName = "default")

参数

+ String timerName - 默认名为"default"
  ,新计时器的名字.用来标记这个计时器,作为参数调用 [Console.timeEnd()](/API/Console/Console/README.md?id=timeEnd)
  可以停止计时并将经过的时间在控制台中打印出来.

返回值:

+ long - 当前时间戳.

示例代码:

+ 在控制台输出当前时间戳.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 获取当前时间戳
def timeStamp = $console.time()
// 输出当前时间戳到控制台
$console.log(timeStamp)
```