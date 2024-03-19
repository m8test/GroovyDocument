功能:

+ 获取 App 版本号

定义:

+ int versionCode()

参数:

+ 无

返回值:

+ int - App 版本号

示例代码:

+ 通过 [AppInfo.versionCode()](/API/App/AppInfo/README.md?id=versionCode) 获取 App 版本号

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
// AppInfo.versionCode() 用于获取 App 版本号
def versionCode = appInfo.versionCode()
$console.log(versionCode)
```