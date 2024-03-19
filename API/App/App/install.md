功能:

+ 安装 App

定义:

+ [App](/API/App/App/README.md) install([ScriptFile](/API/File/ScriptFile/README.md) path)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) path - 需要安装的 App 路径

返回值:

+ [App](/API/App/App/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [App.install()](/API/App/App/README.md?id=install) 安装 App

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.res() 用于配置文件路径为项目资源文件路径
    res("via-release-cn.apk")
}
// App.install() 用于安装 App
$app.install(scriptFile)
```