功能:

+ 判断 App 是否在前台运行

定义:

+ boolean isForeground(String packageName)

参数:

+ String packageName - app 包名

返回值:

+ boolean - 如果 App 在前台运行返回true,否则返回false

示例代码:

+ 通过 [App.isForeground()](/API/App/App/README.md?id=isForeground) 判断 App 是否在前台运行

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.isForeground() 用于判断 App 是否在前台运行
def isForeground = $app.isForeground("com.m8test.main")
$console.log(isForeground)
```