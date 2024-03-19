功能:

+ 获取安卓资源对象

定义:

+ [PackageInfo](https://developer.android.google.cn/reference/android/content/pm/PackageInfo)
  packageInfo()

参数:

+ 无

返回值:

+ [PackageInfo](https://developer.android.google.cn/reference/android/content/pm/PackageInfo) -
  安卓包信息对象

示例代码:

+ 启动一个Activity, 并通过 [ApkPlugin.packageInfo()](/API/Plugin/ApkPlugin/README.md?id=packageInfo)
  方法获取安卓包信息对象

```groovy
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.plugin() 用于配置文件路径为项目插件路径
    plugin("pluginapk.apk")
}
// Plugins.loadApk() 用于将apk作为插件加载
def plugin = $plugins.loadApk(1, scriptFile)
// ApkPlugin.packageInfo() 用于获取安卓包信息对象
def packageInfo = plugin.packageInfo()
// 打印包名
$console.log(packageInfo.packageName)
```