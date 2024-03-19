功能:

+ 获取安卓资源对象

定义:

+ [Resources](https://developer.android.google.cn/reference/android/content/res/Resources)
  resources()

参数:

+ 无

返回值:

+ [Resources](https://developer.android.google.cn/reference/android/content/res/Resources) - 安卓资源对象

示例代码:

+ 启动一个Activity, 并通过 [ApkPlugin.resources()](/API/Plugin/ApkPlugin/README.md?id=resources)
  方法获取安卓资源对象

```groovy
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.plugin() 用于配置文件路径为项目插件路径
    plugin("pluginapk.apk")
}
// Plugins.loadApk() 用于将apk作为插件加载
def plugin = $plugins.loadApk(1, scriptFile)
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
    AsyncImage {
        // delegate -> AsyncImage
        // AsyncImage.request() 用于设置图片请求
        request {
            // delegate -> ImageRequest
            // ApkPlugin.resources() 用于获取安卓资源对象
            def resources = plugin.resources()
            // ImageRequest.drawable() 用于设置从 Drawable 中读取图片
            drawable(resources.getDrawable(resources.getIdentifier("ic_launcher", "mipmap", "com.plugin.pluginapk")))
            // ImageRequest.format() 用于设置图片格式
            format("svg")
        }
    }
}
// Activity.onDestroy() 方法用于监听Activity销毁
$composeActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$composeActivity.start()
```