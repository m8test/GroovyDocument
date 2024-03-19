功能:

+ 获取 App 包名

定义:

+ String packageName()

参数:

+ 无

返回值:

+ String - App 包名

示例代码:

+ 通过 [AppInfo.packageName()](/API/App/AppInfo/README.md?id=packageName) 获取 App 包名

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
// AppInfo.packageName() 用于获取 App 包名
def packageName = appInfo.packageName()
$console.log(packageName)
```