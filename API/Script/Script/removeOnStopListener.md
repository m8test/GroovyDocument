功能:

+ 移除已经添加的脚本停止监听器

定义:

+ boolean removeOnStopListener(int listenerId)

参数:

+ int listenerId -
  待移除的监听器id,即 [Script.addOnStopListener()](/API/Script/Script/README.md?id=addOnStopListener)
  的返回值

返回值:

+ boolean - 移除成功返回true,失败返回false

示例代码:

+ 通过 [Script.removeOnStopListener()](/API/Script/Script/README.md?id=removeOnStopListener)
  方法移除已经添加的脚本停止监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Script.addOnStopListener() 用于添加脚本停止监听器
def listenerId = $script.addOnStopListener {
    $console.log("脚本停止")
}
// Script.removeOnStopListener() 用于移除已经添加的脚本停止监听器
def result = $script.removeOnStopListener(listenerId)
$assert.assertTrue(result, "移除监听器")
// Script.stop() 方法用于停止脚本
$script.stop()
```