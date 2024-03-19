功能:

+ 获取当前脚本主线程.

定义:

+ [ScriptThread](/API/Thread/ScriptThread/README.md) mainThread()

参数:

+ 无

返回值:

+ [ScriptThread](/API/Thread/ScriptThread/README.md) - 脚本主线程对象.

示例代码:

+ 获取脚本主线程并打印线程名到控制台.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 获取脚本主线程
def mainThread = $threads.mainThread()
// 控制台输出脚本主线程名
$console.log(mainThread.name())
// 断言当前线程为主线程
$assert.assertTrue(mainThread == $threads.currentThread(), "当前线程为主线程")
```
