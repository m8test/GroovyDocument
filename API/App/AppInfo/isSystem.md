功能:

+ 判断 App 是否为系统应用

定义:

+ boolean isSystem()

参数:

+ 无

返回值:

+ boolean - 如果 App 为系统应用返回true,否则返回false

示例代码:

+ 通过 [AppInfo.isSystem()](/API/App/AppInfo/README.md?id=isSystem) 判断 App 是否为系统应用

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
// AppInfo.isSystem() 用于判断 App 是否为系统应用
def isSystem = appInfo.isSystem()
$console.log(isSystem)
```