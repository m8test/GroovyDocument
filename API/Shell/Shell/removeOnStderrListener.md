功能:

+ 移除标准错误监听器

定义:

+ boolean removeOnStderrListener(int listenerId)

参数:

+ int listenerId - 监听器Id,也就是 [Shell](/API/Shell/Shell/README.md).adOnStderrListener() 的返回值

返回值:

+ boolean - 移除成功返回true,失败返回false

示例代码:

+ 通过 [Shell.removeOnStderrListener()](/API/Shell/Shell/README.md?id=removeOnStderrListener)
  移除标准错误监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.addOnStderrListener() 用于添加标准错误监听器
def listenerId = shell.addOnStderrListener {
    // it -> String
    $console.log("error line->" + it)
}
// Shell.removeOnStderrListener() 用于移除标准错误监听器
$assert.assertTrue(shell.removeOnStderrListener(listenerId), "移除监听器")
// Shell.exec() 用于执行命令
def shellResult = shell.exec("unknownCommand", null)
// ShellResult.stderr() 用于获取命令执行时所有的标准错误信息
$console.error(shellResult.stderr())
```