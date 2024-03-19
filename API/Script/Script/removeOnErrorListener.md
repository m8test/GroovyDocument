功能:

+ 移除已经添加的脚本错误监听器

定义:

+ boolean removeOnErrorListener(int listenerId)

参数:

+ int listenerId -
  待移除的监听器id,即 [Script.addOnErrorListener()](/API/Script/Script/README.md?id=addOnErrorListener)
  的返回值

返回值:

+ boolean - 移除成功返回true,失败返回false

示例代码:

+ 通过 [Script.removeOnErrorListener()](/API/Script/Script/README.md?id=removeOnErrorListener)
  方法移除已经添加的脚本错误监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Script.addOnErrorListener() 用于添加脚本错误监听器
def listenerId = $script.addOnErrorListener {
    // it -> Throwable
    // Throwable.message() 用于获取异常信息
    $console.log(it.message())
}
// Script.removeOnErrorListener() 用于移除已经添加的脚本错误监听器
def result = $script.removeOnErrorListener(listenerId)
$assert.assertTrue(result, "移除监听器")
1 / 0
```