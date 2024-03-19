功能:

+ 添加脚本错误监听器

定义:

+ int addOnErrorListener(Closure closure)

参数:

+ Closure closure - 设置监听器的闭包
    + 参数
        + [Throwable](/API/Exception/Throwable/README.md) e - 脚本执行错误时的异常对象
    + delegate - 无

返回值:

+ int - 监听器id

示例代码:

+ 通过 [Script.addOnErrorListener()](/API/Script/Script/README.md?id=addOnErrorListener) 方法添加脚本错误监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Script.addOnErrorListener() 用于添加脚本错误监听器
$script.addOnErrorListener {
    // it -> Throwable
    // Throwable.message() 用于获取异常信息
    $console.log(it.message())
}
1 / 0
```