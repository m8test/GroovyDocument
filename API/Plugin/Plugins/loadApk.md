功能:

+ 将apk作为插件加载

定义:

+ [ApkPlugin](/API/Plugin/ApkPlugin/README.md) loadApk(int priority,
  String|[ScriptFile](/API/File/ScriptFile/README.md) apkPath)

参数:

+ int priority - 优先级
+ String|[ScriptFile](/API/File/ScriptFile/README.md) apkPath - apk文件或路径

返回值:

+ [ApkPlugin](/API/Plugin/ApkPlugin/README.md) - 加载后的插件对象

示例代码:

+ 通过 [Plugins.loadApk()](/API/Plugin/Plugins/README.md?id=loadApk) 方法将apk作为插件加载

```groovy
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.plugin() 用于配置文件路径为项目插件路径
    plugin("pluginapk.apk")
}
// Plugins.loadApk() 用于将apk作为插件加载
def plugin = $plugins.loadApk(1, scriptFile)
//def plugin = $plugins.loadApk("/sdcard/plugin/pluginapk.apk")
// ApkPlugin.classLoader() 用于获取类加载器
def classLoader = plugin.classLoader()
// DexClassLoader.loadClass() 用于加载指定的类
def clazz = classLoader.loadClass("com.plugin.pluginapk.Test")
// 创建对象
def apk = clazz.newInstance()
// 调用Native(C/C++)方法
$console.log(apk.getNativeValue())
// 调用实例方法
$console.log(apk.getInstanceValue())
// 调用静态方法
$console.log(apk.getStaticValue())
// 调用静态Native(C/C++)方法
$console.log(apk.getStaticNativeValue())
```