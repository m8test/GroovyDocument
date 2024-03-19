功能:

+ 获取异常信息,可能为null

定义:

+ String message()

参数:

+ 无

返回值:

+ String - 异常信息,可能为null

示例代码:

+ 通过 [Throwable.message()](/API/Exception/Throwable/README.md?id=message) 获取异常信息

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    1 / 0
}.catchAll {
    // Throwable.message() 用于获取异常信息
    $assert.assertTrue(it.message() == "Division by zero", "异常信息")
}
```