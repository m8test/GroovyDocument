功能:

+ 获取 App 支持的最低安卓 Sdk 版本

定义:

+ int minSdkVersion()

参数:

+ 无

返回值:

+ int - App 支持的最低安卓 Sdk 版本

示例代码:

+ 通过 [AppInfo.minSdkVersion()](/API/App/AppInfo/README.md?id=minSdkVersion) 获取 App 支持的最低安卓
  Sdk 版本

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
// AppInfo.minSdkVersion() 用于获取 App 支持的最低安卓 Sdk 版本
def minSdkVersion = appInfo.minSdkVersion()
$console.log(minSdkVersion)
```