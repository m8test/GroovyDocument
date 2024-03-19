功能:

+ 执行命令

定义:

+ [ShellResult](/API/Shell/ShellResult/README.md) exec(
  String|[ShellCommand](/API/Shell/ShellCommand/README.md) command, List<String> arguments)

参数:

+ String|[ShellCommand](/API/Shell/ShellCommand/README.md) command - 需要执行的命令
+ List<String> arguments - 命令执行的参数,如果不需要参数则为 null

返回值:

+ [ShellResult](/API/Shell/ShellResult/README.md) - 命令执行结果

示例代码:

+ 通过 [Shell.exec()](/API/Shell/Shell/README.md?id=exec) 执行命令

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