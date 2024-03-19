功能:

+ 设置脚本文件路径

定义:

+ [ScriptFileConfig](/API/Script/ScriptFileConfig/README.md) file([ScriptFile](/API/File/ScriptFile/README.md) file)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) file - 需要启动的脚本文件

返回值:

+ [ScriptFileConfig](/API/Script/ScriptFileConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [ScriptFileConfig.file()](/API/Script/ScriptFileConfig/README.md?id=file) 方法设置脚本文件路径

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// ScriptEngine.startScriptFile() 用于启动脚本文件
$scriptEngine.startScriptFile {
    // delegate -> ScriptFileConfig
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.res() 用于配置文件路径为项目资源文件路径
        res("scriptFile.groovy")
    }
    // ScriptFileConfig.file() 用于设置脚本文件路径
    file(scriptFile)
}
```