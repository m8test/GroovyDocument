功能:

+ 添加脚本停止监听器

定义:

+ int addOnStopListener(Closure closure)

参数:

+ Closure closure - 设置监听器的闭包
    + 参数 - 无
    + delegate - 无

返回值:

+ int - 监听器id

示例代码:

+ 通过 [Script.addOnStopListener()](/API/Script/Script/README.md?id=addOnStopListener) 方法添加脚本停止监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Script.addOnStopListener() 用于添加脚本停止监听器
$script.addOnStopListener {
    $console.log("脚本停止")
}
// Script.stop() 方法用于停止脚本
$script.stop()
```