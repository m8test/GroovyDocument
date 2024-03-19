功能:

+ 停止脚本

定义:

+ [Script](/API/Script/Script/README.md) stop()

参数:

+ 无

返回值:

+ [Script](/API/Script/Script/README.md) - 返回对象本身翻遍链式调用

示例代码:

+ 通过 [Script.stop()](/API/Script/Script/README.md?id=stop) 方法停止脚本

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