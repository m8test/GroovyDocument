功能:

+ 判断 App 是否正在运行

定义:

+ boolean isRunning(String packageName)

参数:

+ String packageName - app 包名

返回值:

+ boolean - 如果 App 正在运行返回true,否则返回false

示例代码:

+ 通过 [App.isRunning()](/API/App/App/README.md?id=isRunning) 判断 App 是否正在运行

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.isRunning() 用于判断 App 是否正在运行
def isRunning = $app.isRunning("com.m8test.main")
$console.log(isRunning)
```