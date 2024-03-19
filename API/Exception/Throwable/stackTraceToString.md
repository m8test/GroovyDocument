功能:

+ 获取堆栈信息

定义:

+ String stackTraceToString()

参数:

+ 无

返回值:

+ String - 堆栈信息

示例代码:

+ 通过 [Throwable.stackTraceToString()](/API/Exception/Throwable/README.md?id=stackTraceToString)
  获取堆栈信息

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    1 / 0
}.catchAll {
    // Throwable.stackTraceToString() 用于获取堆栈信息
    $console.error(it.stackTraceToString())
}
```