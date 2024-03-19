功能:

+ 启动脚本工程归档文件

定义:

+ [Script](/API/Script/Script/README.md) startScriptProjectArchive(Closure closure)

参数:

+ Closure closure - 设置脚本配置的闭包
    + 参数 - 无
    + delegate - [ScriptProjectArchiveConfig](/API/Script/ScriptProjectArchiveConfig/README.md)

返回值:

+ [Script](/API/Script/Script/README.md) - 返回启动的脚本对象,如果启动脚本失败则返回null

示例代码:

+ 通过
  [ScriptEngine.startScriptProjectArchive()](/API/Script/ScriptEngine/README.md?id=startScriptProjectArchive)
  方法启动脚本工程归档文件

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// ScriptEngine.startScriptProjectArchive() 用于启动脚本工程归档文件
$scriptEngine.startScriptProjectArchive {
    // delegate -> ScriptProjectArchiveConfig
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.res() 用于配置文件路径为项目资源文件路径
        res("com.example.app.spa")
    }
    // ScriptProjectArchiveConfig.path() 用于设置脚本工程归档文件路径
    path(scriptFile)
}
```