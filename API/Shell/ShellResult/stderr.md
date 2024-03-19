功能:

+ 获取命令执行时所有的标准错误信息

定义:

+ List\<String\> stderr()

参数:

+ 无

返回值:

+ List\<String\> - 命令执行时所有的标准错误信息

示例代码:

+ 通过 [ShellResult.stderr()](/API/Shell/ShellResult/README.md?id=stderr) 获取命令执行时所有的标准错误信息

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.exec() 用于执行命令
def shellResult = shell.exec("unknownCommand", null)
// ShellResult.stderr() 用于获取命令执行时所有的标准错误信息
$console.error(shellResult.stderr())
```