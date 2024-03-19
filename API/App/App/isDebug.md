功能:

+ 判断 App 是否用于调试

定义:

+ boolean isDebug(String packageName)

参数:

+ String packageName - app 包名

返回值:

+ boolean - 如果 App 用于调试返回true,否则返回false

示例代码:

+ 通过 [App.isDebug()](/API/App/App/README.md?id=isDebug) 判断 App 是否用于调试

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.isDebug() 用于判断 App 是否用于调试
def isDebug = $app.isDebug("com.m8test.main")
$console.log(isDebug)
```