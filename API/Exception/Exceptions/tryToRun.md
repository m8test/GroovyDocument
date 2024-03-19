功能:

+ 运行闭包并捕获该闭包中产生的异常.

定义:

+ [Trier](/API/Exception/Trier/README.md) tryToRun(Closure runnable)

参数:

+ Closure runnable - 需要运行的闭包
    + 参数
        + [Throwable](/API/Exception/Throwable/README.md) e - 捕获到的异常
    + delegate - 无

返回值:

+ [Trier](/API/Exception/Trier/README.md) - 对异常进行处理的对象

示例代码:

+ 通过 [Exceptions.tryToRun()](/API/Exception/Exceptions/README.md?id=tryToRun) 运行闭包并捕获该闭包中产生的异常.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    1 / 0
}.catchAll {
    // 如果出现异常,会执行此闭包的代码
    $console.log("捕获到异常:${it.message()}")
}
```