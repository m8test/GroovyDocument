功能:

+ 将jar作为插件加载

定义:

+ [DexPlugin](/API/Plugin/DexPlugin/README.md) loadJar(int priority,
  String|[ScriptFile](/API/File/ScriptFile/README.md) jarPath)

参数:

+ int priority - 优先级
+ String|[ScriptFile](/API/File/ScriptFile/README.md) jarPath - jar文件或路径

返回值:

+ [DexPlugin](/API/Plugin/DexPlugin/README.md) - 加载后的插件对象

示例代码:

+ 通过 [Plugins.loadJar()](/API/Plugin/Plugins/README.md?id=loadJar) 方法将jar作为插件加载

```groovy
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.plugin() 用于配置文件路径为项目插件路径
    plugin("pluginjar.jar")
}
// Plugins.loadJar() 用于将jar作为插件加载
def plugin = $plugins.loadJar(1, scriptFile)
//def plugin = $plugins.loadJar(1, "/sdcard/plugin/pluginjar.jar")
// DexPlugin.classLoader() 用于获取类加载器
def classLoader = plugin.classLoader()
// DexClassLoader.loadClass() 用于加载指定的类
def clazz = classLoader.loadClass("com.plugin.pluginjar.Test")
// 创建对象
def jar = clazz.newInstance()
// 调用实例方法
$console.log(jar.getInstanceValue())
// 调用静态方法
$console.log(jar.getStaticValue())
```