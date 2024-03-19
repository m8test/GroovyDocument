功能:

+ 注册处理器供 WebView 端调用

定义:

+ [WebViewBridge](/API/UI/WebView/WebViewBridge/README.md) registerHandler(String handlerName,
  Closure closure)

参数:

+ String handlerName - 处理器名,如果handlerName重复则会覆盖之前设置的处理器
+ Closure closure - 处理器实际执行的代码闭包
    + 参数
        + String params - WebView 端调用处理器时传递的参数,可以为null
    + 返回值
        + String - 返回到 WebView 端的值,可以为null

返回值:

+ [WebViewBridge](/API/UI/WebView/WebViewBridge/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  通过 [WebViewBridge.registerHandler()](/API/UI/WebView/WebViewBridge/README.md?id=registerHandler)
  方法注册处理器供 WebView 端调用

```groovy
// WebViewActivity.webViewBridge() 用于获取 WebViewBridge 对象
def bridge = $webViewActivity.webViewBridge()
// WebViewBridge.registerHandler() 用于注册处理器供 WebView 端调用
bridge.registerHandler("handlerForWebView") {
    // it -> String
    // it 表示从 WebView 端传来的参数,如果没有则为 null
    def paramFromWebView = it
    // 返回内容到 WebView 端,只能是字符串或者null
    return "$paramFromWebView return from script"
}
// Activity.onDestroy() 方法用于监听Activity销毁
$webViewActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$webViewActivity.start()
```