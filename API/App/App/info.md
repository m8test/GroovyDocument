功能:

+ 获取 App 信息

定义:

+ [AppInfo](/API/App/AppInfo/README.md) info(String packageName)

参数:

+ String packageName - app 包名

返回值:

+ [AppInfo](/API/App/AppInfo/README.md) - App 信息

示例代码:

+ 通过 [App.info()](/API/App/App/README.md?id=info) 获取 App 信息

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
$console.log(appInfo)
```