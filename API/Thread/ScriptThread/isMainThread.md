功能:

+ 判断是否为脚本主线程.

定义:

+ boolean isMainThread()

参数:

+ 无

返回值:

+ boolean - 如果是脚本主线程返回true,否则返回false

示例代码:

+ 通过 [ScriptThread.isMainThread()](/API/Thread/ScriptThread/README.md?id=isMainThread) 方法判断是否为脚本主线程

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 开启一个子线程不指定线程名
$threads.startThread {
    // 获取当前线程对象
    def currentThread = $threads.currentThread()
    // ScriptThread.isMainThread() 用于判断是否为脚本主线程
    $assert.assertFalse(currentThread.isMainThread())
}
// 获取当前线程对象
def currentThread = $threads.currentThread()
// ScriptThread.isMainThread() 用于判断是否为脚本主线程
$assert.assertTrue(currentThread.isMainThread())
```