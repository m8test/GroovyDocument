功能:

+ 获取 App 名称

定义:

+ String name()

参数:

+ 无

返回值:

+ String - App 名称

示例代码:

+ 通过 [AppInfo.name()](/API/App/AppInfo/README.md?id=name) 获取 App 名称

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
// AppInfo.name() 用于获取 App 名称
def name = appInfo.name()
$console.log(name)
```