功能:

+ 移除已经添加的脚本完成监听器

定义:

+ boolean removeOnFinishListener(int listenerId)

参数:

+ int listenerId -
  待移除的监听器id,即 [Script.addOnFinishListener()](/API/Script/Script/README.md?id=addOnFinishListener)
  的返回值

返回值:

+ boolean - 移除成功返回true,失败返回false

示例代码:

+ 通过 [Script.removeOnFinishListener()](/API/Script/Script/README.md?id=removeOnFinishListener)
  方法移除已经添加的脚本完成监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Script.addOnFinishListener() 用于添加脚本完成监听器
def listenerId = $script.addOnFinishListener { result ->
    $assert.assertTrue(result, "脚本执行结果")
}
// Script.removeOnFinishListener() 用于移除已经添加的脚本完成监听器
def result = $script.removeOnFinishListener(listenerId)
$assert.assertTrue(result, "移除监听器")
true
```