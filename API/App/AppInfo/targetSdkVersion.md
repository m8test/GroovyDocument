功能:

+ 获取 App 目标 Sdk 版本

定义:

+ int targetSdkVersion()

参数:

+ 无

返回值:

+ int - App 目标 Sdk 版本

示例代码:

+ 通过 [AppInfo.targetSdkVersion()](/API/App/AppInfo/README.md?id=targetSdkVersion) 获取 App 目标
  Sdk 版本

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
// AppInfo.targetSdkVersion() 用于获取 App 目标 Sdk 版本
def targetSdkVersion = appInfo.targetSdkVersion()
$console.log(targetSdkVersion)
```