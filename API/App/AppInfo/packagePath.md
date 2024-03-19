功能:

+ 获取 App 包路径

定义:

+ String packagePath()

参数:

+ 无

返回值:

+ String - App 包路径

示例代码:

+ 通过 [AppInfo.packagePath()](/API/App/AppInfo/README.md?id=packagePath) 获取 App 包路径

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
// AppInfo.packagePath() 用于获取 App 包路径
def packagePath = appInfo.packagePath()
$console.log(packagePath)
```