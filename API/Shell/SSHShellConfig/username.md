功能:

+ 设置 SSH 服务器用户名

定义:

+ [SSHShellConfig](/API/Shell/SSHShellConfig/README.md) username(String username)

参数:

+ String username - SSH 服务器用户名

返回值:

+ [SSHShellConfig](/API/Shell/SSHShellConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [SSHShellConfig.username()](/API/Shell/SSHShellConfig/README.md?id=username) 设置 SSH 服务器用户名

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
