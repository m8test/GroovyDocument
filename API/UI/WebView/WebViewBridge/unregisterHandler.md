功能:

+ 取消注册处理器

定义:

+ boolean unregisterHandler(String handlerName)

参数:

+ String handlerName - 处理器名,如果handlerName不存在则返回false

返回值:

+ boolean - 取消注册成功返回true,否则返回false

示例代码:

+ 启动一个Activity,
  通过 [WebViewBridge.unregisterHandler()](/API/UI/WebView/WebViewBridge/README.md?id=unregisterHandler)
  方法取消注册处理器

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
// WebViewBridge.registerHandler() 用于注册处理器供 WebView 端调用
bridge.registerHandler("unregisterHandler") {
    // WebViewBridge.unregisterHandler() 用于取消注册处理器
    bridge.unregisterHandler("handlerForWebView")
}
// Activity.onDestroy() 方法用于监听Activity销毁
$webViewActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$webViewActivity.start()
```