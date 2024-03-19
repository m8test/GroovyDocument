功能:

+ 获取类加载器

定义:

+ [DexClassLoader](https://developer.android.google.cn/reference/dalvik/system/DexClassLoader)
  classLoader()

参数:

+ 无

返回值:

+ [DexClassLoader](https://developer.android.google.cn/reference/dalvik/system/DexClassLoader) -
  插件的类加载器

示例代码:

+ 通过 [DexPlugin.classLoader()](/API/Plugin/DexPlugin/README.md?id=classLoader) 方法获取类加载器

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