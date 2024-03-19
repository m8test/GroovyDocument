功能:

+ 将dex作为插件加载

定义:

+ [DexPlugin](/API/Plugin/DexPlugin/README.md) loadDex(int priority,
  String|[ScriptFile](/API/File/ScriptFile/README.md) dexPath,
  String|[ScriptFile](/API/File/ScriptFile/README.md) soPath = null)

参数:

+ int priority - 优先级
+ String|[ScriptFile](/API/File/ScriptFile/README.md) dexPath - dex文件或路径
+ String|[ScriptFile](/API/File/ScriptFile/README.md) soPath - so文件所在的路径或文件,默认为null

返回值:

+ [DexPlugin](/API/Plugin/DexPlugin/README.md) - 加载后的插件对象

示例代码:

+ 通过 [Plugins.loadDex()](/API/Plugin/Plugins/README.md?id=loadDex) 方法将dex作为插件加载

```groovy
// Device.system() 用于获取System对象
def system = $device.system()
// System.supportedABIs() 用于获取设备所有支持的ABI
def abis = system.supportedABIs()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def dexFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.plugin() 用于配置文件路径为项目插件路径
    plugin("plugindex.dex")
}
// Files.buildFile() 用于构建一个 ScriptFile 对象
def soPath = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.plugin() 用于配置文件路径为项目插件路径
    plugin(abis[0])
}
// Plugins.loadDex() 用于将dex作为插件加载
def plugin = $plugins.loadDex(1, dexFile, soPath)
//def plugin = $plugins.loadDex(1, "/sdcard/plugin/plugindex.dex", "/sdcard/plugin/lib/${abis[0]}/")
// DexPlugin.classLoader() 用于获取类加载器
def classLoader = plugin.classLoader()
// DexClassLoader.loadClass() 用于加载指定的类
def clazz = classLoader.loadClass("com.plugin.pluginapk.Test")
// 创建对象
def dex = clazz.newInstance()
// 调用Native(C/C++)方法
$console.log(dex.getNativeValue())
// 调用实例方法
$console.log(dex.getInstanceValue())
// 调用静态方法
$console.log(dex.getStaticValue())
// 调用静态Native(C/C++)方法
$console.log(dex.getStaticNativeValue())
```