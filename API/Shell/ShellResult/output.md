功能:

+ 获取命令执行时所有的输出信息

定义:

+ List\<String\> output()

参数:

+ 无

返回值:

+ List\<String\> - 命令执行时所有的输出信息

示例代码:

+ 通过 [ShellResult.output()](/API/Shell/ShellResult/README.md?id=output) 获取命令执行时所有的输出信息

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.exec() 用于执行命令
def shellResult = shell.exec("echo", ["\$\$"])
// ShellResult.output() 用于获取命令执行时所有的输出信息
$console.log(shellResult.output())
```