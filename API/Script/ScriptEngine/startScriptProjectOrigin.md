功能:

+ 启动原始脚本工程

定义:

+ [Script](/API/Script/Script/README.md) startScriptProjectOrigin(Closure closure)

参数:

+ Closure closure - 设置脚本配置的闭包
    + 参数 - 无
    + delegate - [ScriptProjectOriginConfig](/API/Script/ScriptProjectOriginConfig/README.md)

返回值:

+ [Script](/API/Script/Script/README.md) - 返回启动的脚本对象,如果启动脚本失败则返回null

示例代码:

+ 通过
  [ScriptEngine.startScriptProjectOrigin()](/API/Script/ScriptEngine/README.md?id=startScriptProjectOrigin)
  方法启动原始脚本工程

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// ScriptEngine.startScriptProjectOrigin() 用于启动原始脚本工程
$scriptEngine.startScriptProjectOrigin {
    // delegate -> ScriptProjectOriginConfig
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.res() 用于配置文件路径为项目资源文件路径
        res("com.example.app")
    }
    // ScriptProjectOriginConfig.path() 用于设置原始脚本工程路径
    path(scriptFile)
}
```