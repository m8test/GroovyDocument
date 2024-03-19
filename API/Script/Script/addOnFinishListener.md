功能:

+ 添加脚本完成监听器

定义:

+ int addOnFinishListener(Closure closure)

参数:

+ Closure closure - 设置监听器的闭包
    + 参数
        + Object result - 脚本执行结果
    + delegate - 无

返回值:

+ int - 监听器id

示例代码:

+ 通过 [Script.addOnFinishListener()](/API/Script/Script/README.md?id=addOnFinishListener)
  方法添加脚本完成监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Script.addOnFinishListener() 用于添加脚本完成监听器
$script.addOnFinishListener { result ->
    $assert.assertTrue(result, "脚本执行结果")
}
true
```