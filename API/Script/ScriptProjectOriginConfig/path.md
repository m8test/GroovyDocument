功能:

+ 设置原始脚本工程路径

定义:

+ [ScriptProjectOriginConfig](/API/Script/ScriptProjectOriginConfig/README.md)
  path([ScriptFile](/API/File/ScriptFile/README.md) path)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) path - 待启动的原始脚本工程路径

返回值:

+ [ScriptProjectOriginConfig](/API/Script/ScriptProjectOriginConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [ScriptProjectOriginConfig.path()](/API/Script/ScriptProjectOriginConfig/README.md?id=path)
  方法设置原始脚本工程路径

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