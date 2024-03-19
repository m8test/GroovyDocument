功能:

+ 检查 [Shell](/API/Shell/Shell/README.md) 是否已关闭

定义:

+ boolean isShutdown()

参数:

+ 无

返回值:

+ boolean - 如果 [Shell](/API/Shell/Shell/README.md) 已关闭返回true,否则返回false

示例代码:

+ 通过 [Shell.isShutdown()](/API/Shell/Shell/README.md?id=isShutdown)
  检查 [Shell](/API/Shell/Shell/README.md) 是否已关闭

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.exec() 用于执行命令
def shellResult = shell.exec("echo", ["\$\$"])
// ShellResult.output() 用于获取命令执行时所有的输出信息
$console.log(shellResult.output())
// Shell.isShutdown() 用于检查 Shell 是否已关闭
$assert.assertFalse(shell.isShutdown(), "Shell 没有关闭")
// Shell.shutdown() 用于关闭 Shell
shell.shutdown()
// Shell.isShutdown() 用于检查 Shell 是否已关闭
$assert.assertTrue(shell.isShutdown(), "Shell 已关闭")
```