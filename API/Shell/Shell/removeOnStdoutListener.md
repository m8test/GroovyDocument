功能:

+ 移除标准输出监听器

定义:

+ boolean removeOnStdoutListener(int listenerId)

参数:

+ int listenerId - 监听器Id,也就是 [Shell](/API/Shell/Shell/README.md).adOnStdoutListener() 的返回值

返回值:

+ boolean - 移除成功返回true,失败返回false

示例代码:

+ 通过 [Shell.removeOnStdoutListener()](/API/Shell/Shell/README.md?id=removeOnStdoutListener)
  移除标准输出监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.addOnStdoutListener() 用于添加标准输出监听器
def listenerId = shell.addOnStdoutListener {
    // it -> String
    $console.log("stdout line->" + it)
}
// Shell.removeOnStdoutListener() 用于移除标准输出监听器
$assert.assertTrue(shell.removeOnStdoutListener(listenerId), "移除监听器")
// Shell.exec() 用于执行命令
def shellResult = shell.exec("echo", ["\$\$"])
// ShellResult.stdout() 用于获取命令执行时所有的标准输出输出信息
$console.log(shellResult.stdout())
```