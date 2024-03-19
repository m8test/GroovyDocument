功能:

+ 判断包名是否已经安装

定义:

+ boolean isPackageInstalled(String packageName)

参数:

+ String packageName - 脚本工程包名

返回值:

+ boolean - true表示已安装,false表示未安装

示例代码:

+ 通过 [ScriptEngine.isPackageInstalled()](/API/Script/ScriptEngine/README.md?id=isPackageInstalled)
  方法判断包名是否已经安装

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