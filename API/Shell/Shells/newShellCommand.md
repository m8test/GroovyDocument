功能:

+ 创建 [Shell](/API/Shell/Shell/README.md) 命令

定义:

+ [ShellCommand](/API/Shell/ShellCommand/README.md)
  newShellCommand([ScriptFile](/API/File/ScriptFile/README.md) file)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) file - 命令所在路径

返回值:

+ [ShellCommand](/API/Shell/ShellCommand/README.md) -
  根据文件创建的 [Shell](/API/Shell/Shell/README.md) 命令,如果创建失败会抛异常

示例代码:

+ 通过 [Shells.newShellCommand()](/API/Shell/Shells/README.md?id=newShellCommand)
  创建 [Shell](/API/Shell/Shell/README.md) 命令,实现
  frp 内网穿透

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.addOnStderrListener() 用于添加标准错误监听器
shell.addOnStderrListener {
    // it -> String
    $console.error(it)
}
// Shell.addOnStdoutListener() 用于添加标准输出监听器
shell.addOnStdoutListener {
    // it -> String
    $console.log(it)
}
// Device.system() 用于获取System对象
def system = $device.system()
// System.supportedABIs() 用于获取设备所有支持的ABI
def abis = system.supportedABIs()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def frpcBin = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.res() 用于配置文件路径为项目资源文件路径
    res("${abis[0]}/frpc")
}
// Files.buildFile() 用于构建一个 ScriptFile 对象
def frpcConfig = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.res() 用于配置文件路径为项目资源文件路径
    res("frpc.ini")
}
// Files.buildFile() 用于构建一个 ScriptFile 对象
def frpcConfigCopied = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path("/sdcard/frpc.ini")
}
// ScriptFile.copyTo() 用于复制文件
frpcConfig.copyTo(frpcConfigCopied, true)
// Shells.newShellCommand() 用于创建 Shell 命令
def command = $shells.newShellCommand(frpcBin)
// Shell.exec() 用于执行命令
def shellResult = shell.exec(command, ["-c", frpcConfigCopied.canonicalPath()])
// ShellResult.output() 用于获取命令执行时所有的输出信息
$console.log(shellResult.output())
```
