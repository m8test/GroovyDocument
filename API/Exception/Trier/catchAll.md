功能:

+ 捕获 [Exceptions.tryToRun()](/API/Exception/Exceptions/README.md?id=tryToRun)
  可能产生的异常.如果没有异常产生那么此方法不会被调用

定义:

+ [Trier](/API/Exception/Trier/README.md) catchAll(Closure closure)

参数:

+ Closure closure - 产生异常时调用的闭包
    + 参数
        + [Throwable](/API/Exception/Throwable/README.md) e - 捕获到的异常对象
    + delegate - 无

返回值:

+ [Trier](/API/Exception/Trier/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [Trier.catchAll()](/API/Exception/Trier/README.md?id=catchAll)
  捕获 [Exceptions.tryToRun()](/API/Exception/Exceptions/README.md?id=tryToRun) 可能产生的异常

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    1 / 0
}.catchAll {
    $console.error("产生异常")
    // Throwable.cause() 用于获取导致此 Throwable 的原因.
    $assert.assertTrue(it.cause() == null, "原因为null")
}
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    $console.log("没有异常")
}.catchAll {
    $console.error("没有异常产生,此代码不会被执行")
    // Throwable.cause() 用于获取导致此 Throwable 的原因.
    $assert.assertTrue(it.cause() == null, "原因为null")
}
```