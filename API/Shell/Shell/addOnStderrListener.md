功能:

+ 添加标准错误监听器

定义:

+ int addOnStderrListener(Closure closure)

参数:

+ Closure closure - 设置监听器的闭包
    + 参数
        + String line - 标准错误的行信息
    + delegate - 无

返回值:

+ int - 监听器id

示例代码:

+ 通过 [Shell.addOnStderrListener()](/API/Shell/Shell/README.md?id=addOnStderrListener) 添加标准错误监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.addOnStderrListener() 用于添加标准错误监听器
shell.addOnStderrListener {
    // it -> String
    $console.log("error line->" + it)
}
// Shell.exec() 用于执行命令
def shellResult = shell.exec("unknownCommand", null)
// ShellResult.stderr() 用于获取命令执行时所有的标准错误信息
$console.error(shellResult.stderr())
```