功能:

+ 获取 App 用户ID

定义:

+ int uid(String packageName)

参数:

+ String packageName - app 包名

返回值:

+ int - 用户ID

示例代码:

+ 通过 [App.uid()](/API/App/App/README.md?id=uid) 获取 App 用户ID

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// App.uid() 用于获取 App 用户ID
def uid = $app.uid("com.m8test.main")
$console.log(uid)
```