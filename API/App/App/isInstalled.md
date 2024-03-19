功能:

+ 判断 App 是否已安装

定义:

+ boolean isInstalled(String packageName)

参数:

+ String packageName - app 包名

返回值:

+ boolean - 如果 App 已安装返回true,否则返回false

示例代码:

+ 通过 [App.isInstalled()](/API/App/App/README.md?id=isInstalled) 判断 App 是否已安装

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.isInstalled() 用于判断 App 是否已安装
def isInstalled = $app.isInstalled("com.m8test.main")
$console.log(isInstalled)
```