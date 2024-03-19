功能:

+ 启动 App

定义:

+ [App](/API/App/App/README.md) launch(String packageName)

参数:

+ String packageName - app 包名

返回值:

+ [App](/API/App/App/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [App.launch()](/API/App/App/README.md?id=launch) 启动 App

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.launch() 用于启动 App
$app.launch("com.m8test.main")
```