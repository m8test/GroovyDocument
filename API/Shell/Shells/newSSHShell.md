功能:

+ 创建一个新的 SSH [Shell](/API/Shell/Shell/README.md)

定义:

+ [Shell](/API/Shell/Shell/README.md) newSSHShell(Closure closure)

参数:

+ Closure closure - 配置 SSH [Shell](/API/Shell/Shell/README.md) 的闭包
    + 参数 - 无
    + delegate - [SSHShellConfig](/API/Shell/SSHShellConfig/README.md)

返回值:

+ [Shell](/API/Shell/Shell/README.md) - 根据配置创建的 [Shell](/API/Shell/Shell/README.md)
  对象,如果创建失败返回null

示例代码:

+ 通过 [Shells.newSSHShell()](/API/Shell/Shells/README.md?id=newSSHShell) 创建一个新的
  SSH [Shell](/API/Shell/Shell/README.md)

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Shells.newSSHShell() 用于创建一个新的 SSH Shell
def shell = $shells.newSSHShell {
    // delegate -> SSHShellConfig
    // SSHShellConfig.host() 用于设置 SSH 服务器主机地址(ip/domain)
    host("127.0.0.1")
    // SSHShellConfig.port() 用于设置 SSH 服务器主机端口号
    port(2202)
    // SSHShellConfig.username() 用于设置 SSH 服务器用户名
    username("M8Test")
    // SSHShellConfig.password() 用于设置 SSH 服务器密码
    password("com.m8test.main")
}
// Shell.exec() 用于执行命令
def shellResult = shell.exec("echo", ["\$\$"])
// ShellResult.output() 用于获取命令执行时所有的输出信息
$console.log(shellResult.output())
```