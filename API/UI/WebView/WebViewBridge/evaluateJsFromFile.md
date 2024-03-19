功能:

+ 在 WebView 端执行js文件

定义:

+ boolean evaluateJsFromFile([ScriptFile](/API/File/ScriptFile/README.md) path, boolean repeatable,
  Closure closure)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) path - 需要执行的js文件路径
+ boolean repeatable - 在一个页面中是否允许多次执行
+ Closure closure - 执行完js文件后回调的闭包,可以为null
    + 参数
        + String result - 执行js文件的结果,可以为null
    + 返回值 - 无

返回值:

+ boolean - 执行成功返回true,失败返回false

示例代码:

+ 启动一个Activity,
  通过 [WebViewBridge.evaluateJsFromFile()](/API/UI/WebView/WebViewBridge/README.md?id=evaluateJsFromFile)
  方法在 WebView 端执行js文件

```groovy
// WebViewActivity.webViewBridge() 用于获取 WebViewBridge 对象
def bridge = $webViewActivity.webViewBridge()
// WebViewBridge.registerHandler() 用于注册处理器供 WebView 端调用
bridge.registerHandler("handlerForWebView") {
    // it -> String
    // it 表示从 WebView 端传来的参数,如果没有则为 null
    def paramFromWebView = it
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def jsFilePath = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.res() 用于配置文件路径为项目资源文件路径
        res("inject.js")
    }
    // WebViewBridge.evaluateJsFromFile() 用于在 WebView 端执行js文件
    bridge.evaluateJsFromFile(jsFilePath, false) {
        $console.log("执行js文件结果:$it")
    }
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