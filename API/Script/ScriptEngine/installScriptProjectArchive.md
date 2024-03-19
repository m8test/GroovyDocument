功能:

+ 安装脚本工程归档文件,安装以后可以通过
  [ScriptEngine.startScriptProjectInstalled()](/API/Script/ScriptEngine/README.md?id=startScriptProjectInstalled)
  启动

定义:

+ boolean installScriptProjectArchive([ScriptFile](/API/File/ScriptFile/README.md) path, boolean
  override)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) path - 待安装的脚本工程归档文件路径
+ boolean override - 如果该脚本工程已经安装,是否需要覆盖安装

返回值:

+ boolean - true表示安装成功,false表示安装失败

示例代码:

+ 通过
  [ScriptEngine.installScriptProjectArchive()](/API/Script/ScriptEngine/README.md?id=installScriptProjectArchive)
  方法安装脚本工程归档文件

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
def projectPackageName = "com.example.app"
// ScriptEngine.isPackageInstalled() 用于判断包名是否已经安装
def isPackageInstalled = $scriptEngine.isPackageInstalled(projectPackageName)
if (!isPackageInstalled) {
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.res() 用于配置文件路径为项目资源文件路径
        res("com.example.app.spa")
    }
    // ScriptEngine.installScriptProjectArchive() 用于安装脚本工程归档文件
    $scriptEngine.installScriptProjectArchive(scriptFile, false)
}
// ScriptEngine.startScriptProjectInstalled() 用于启动已安装的脚本工程
$scriptEngine.startScriptProjectInstalled {
    // delegate -> ScriptProjectInstalledConfig
    // ScriptProjectInstalledConfig.packageName() 用于设置需要启动的脚本工程包名
    packageName(projectPackageName)
}
```