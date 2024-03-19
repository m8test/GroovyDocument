功能:

+ 获取 App 版本名称

定义:

+ String versionName()

参数:

+ 无

返回值:

+ String - App 版本名称

示例代码:

+ 通过 [AppInfo.versionName()](/API/App/AppInfo/README.md?id=versionName) 获取 App 版本名称

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
// AppInfo.versionName() 用于获取 App 版本名称
def versionName = appInfo.versionName()
$console.log(versionName)
```