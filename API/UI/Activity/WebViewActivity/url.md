功能:

+ 设置 WebView 显示(脚本界面)的 url 地址,用此方法可以将一个网页作为脚本的界面,如果需要更新界面则无需更新脚本内容,只需要更新网站内容即可

定义:

+ [WebViewActivity](/API/UI/Activity/WebViewActivity/README.md) url(String url)

参数:

+ String url - 需要设置为界面的网页url地址

返回值:

+ [WebViewActivity](/API/UI/Activity/WebViewActivity/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 通过 [WebViewActivity.url()](/API/UI/Activity/WebViewActivity/README.md?id=url)
  方法设置 WebView 显示(脚本界面)的 url 地址

```groovy
// WebViewActivity.url() 用于设置 WebView 显示(脚本界面)的 url 地址
$webViewActivity.url("https://www.baidu.com")
// Activity.onDestroy() 方法用于监听Activity销毁
$webViewActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$webViewActivity.start()
```