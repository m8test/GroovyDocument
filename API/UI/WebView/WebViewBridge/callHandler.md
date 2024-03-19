功能:

+ 调用 WebView 端注册的处理器

定义:

+ boolean callHandler(String handlerName, String params, Closure closure)

参数:

+ String handlerName - WebView 端注册的处理器名
+ String params - 传递给该处理器的参数
+ Closure closure - 处理 WebView 端处理器返回值的闭包
    + 参数
        + String returnValue - WebView 端处理器返回结果
    + 返回值 - 无

返回值:

+ boolean - 调用成功返回true,失败返回false

示例代码:

+ 启动一个Activity,
  通过 [WebViewBridge.callHandler()](/API/UI/WebView/WebViewBridge/README.md?id=callHandler) 方法调用
  WebView 端注册的处理器

```groovy
// WebViewActivity.webViewBridge() 用于获取 WebViewBridge 对象
def bridge = $webViewActivity.webViewBridge()
// WebViewBridge.registerHandler() 用于注册处理器供 WebView 端调用
bridge.registerHandler("handlerForWebView") {
    // it -> String
    // it 表示从 WebView 端传来的参数,如果没有则为 null
    def paramFromWebView = it
    def handledParams = "$paramFromWebView return from script"
    // WebViewBridge.callHandler() 用于调用 WebView 端注册的处理器
    bridge.callHandler("functionForScriptToCall", handledParams) {
        // it -> String
        // it 为 WebView 端js函数返回值
        // Toast.showShort() 用于显示短吐司
        $toast.showShort(it)
    }
}
// Activity.onDestroy() 方法用于监听Activity销毁
$webViewActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$webViewActivity.start()
```