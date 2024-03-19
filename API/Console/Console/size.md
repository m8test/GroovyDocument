功能:

+ 设置/获取日志容量(默认情况下不限制容量大小)

定义:

+ int|[Console](/API/Console/Console/README.md) size(int capacity)

参数

+ int capacity - 如果不设置capacity参数,则会获取当前日志容量,如果设置capacity,则会设置日志容量大小为capacity

返回值:

+ int - 如果不设置capacity参数,那么返回当前日志容量.
+ [Console](/API/Console/Console/README.md) - 如果设置capacity参数,那么返回对象本身,方便链式调用.

示例代码:

+ 设置控制台日志容量大小为5,每隔300毫秒输出一条日志,总共输出10条.由于控制台容量大小为5,当日志容量超过5时,最早输出的日志会被移除.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 设置控制台最多只显示5条日志
$console.size(5)
// 打印当前日志容量,结果为5
$console.log("日志容量为:" + $console.size())
// 输出10条日志,每个300毫秒输出一条日志,如果当前日志超过5,最早输出的日志会自动被删除
for (i in 0..<10) {
    $console.log(i)
    $threads.sleep(300)
}
```