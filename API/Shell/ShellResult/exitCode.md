功能:

+ 获取命令执行结果退出码

定义:

+ int exitCode()

参数:

+ 无

返回值:

+ int - 命令执行结果退出码

示例代码:

+ 通过 [ShellResult.exitCode()](/API/Shell/ShellResult/README.md?id=exitCode) 获取命令执行结果退出码

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.exec() 用于执行命令
def shellResult = shell.exec("echo", ["\$\$"])
// ShellResult.exitCode() 用于获取命令执行结果退出码
$console.log(shellResult.exitCode())
```