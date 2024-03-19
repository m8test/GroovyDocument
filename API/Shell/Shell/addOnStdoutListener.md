功能:

+ 添加标准输出监听器

定义:

+ int addOnStdoutListener(Closure closure)

参数:

+ Closure closure - 设置监听器的闭包
    + 参数
        + String line - 标准输出的行信息
    + delegate - 无

返回值:

+ int - 监听器id

示例代码:

+ 通过 [Shell.addOnStdoutListener()](/API/Shell/Shell/README.md?id=addOnStdoutListener) 添加标准输出监听器

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newLocalShell() 用于创建一个新的本地 Shell
def shell = $shells.newLocalShell("application")
// Shell.addOnStdoutListener() 用于添加标准输出监听器
shell.addOnStdoutListener {
    // it -> String
    $console.log("stdout line->" + it)
}
// Shell.exec() 用于执行命令
def shellResult = shell.exec("echo", ["\$\$"])
// ShellResult.stdout() 用于获取命令执行时所有的标准输出输出信息
$console.log(shellResult.stdout())
```