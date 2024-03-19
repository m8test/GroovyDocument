功能:

+ 检查 [Shell](/API/Shell/Shell/README.md) 是否处于空闲状态

定义:

+ boolean isIdle()

参数:

+ 无

返回值:

+ boolean - 如果 [Shell](/API/Shell/Shell/README.md) 处于空闲状态返回true,否则返回false

示例代码:

+ 通过 [Shell.isIdle()](/API/Shell/Shell/README.md?id=isIdle)
  检查 [Shell](/API/Shell/Shell/README.md) 是否处于空闲状态

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.isIdle() 用于检查 Shell 是否处于空闲状态
$console.log("isIdle->" + shell.isIdle())
// Shell.exec() 用于执行命令
def shellResult = shell.exec("echo", ["\$\$"])
// ShellResult.output() 用于获取命令执行时所有的输出信息
$console.log(shellResult.output())
```