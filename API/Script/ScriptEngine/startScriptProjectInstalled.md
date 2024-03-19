功能:

+ 启动已安装的脚本工程

定义:

+ [Script](/API/Script/Script/README.md) startScriptProjectInstalled(Closure closure)

参数:

+ Closure closure - 设置脚本配置的闭包
    + 参数 - 无
    + delegate - [ScriptProjectInstalledConfig](/API/Script/ScriptProjectInstalledConfig/README.md)

返回值:

+ [Script](/API/Script/Script/README.md) - 返回启动的脚本对象,如果启动脚本失败则返回null

示例代码:

+ 通过
  [ScriptEngine.startScriptProjectInstalled()](/API/Script/ScriptEngine/README.md?id=startScriptProjectInstalled)
  方法启动已安装的脚本工程

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