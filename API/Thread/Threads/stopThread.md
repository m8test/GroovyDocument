功能:

+ 停止线程

定义:

+ boolean stopThread([ScriptThread](/API/Thread/ScriptThread/README.md) scriptThread)

参数:

+ [ScriptThread](/API/Thread/ScriptThread/README.md) scriptThread - 需要停止的线程对象

返回值:

+ boolean
    + true - 如果待停止线程正在运行则将其停止并返回true
    + false - 如果待停止线程已经停止运行或者之前被停止过则返回false

示例代码:

+ 开启一个子线程每100毫秒输出一次,主线程睡眠300毫秒后将该子线程结束,原本会输出10次才停止的子线程只会输出3次就停止了.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 开启一个子线程,主线程会等待所有子线程结束运行后再结束运行
def scriptThread = $threads.startThread {
    // 断言当前线程不是主线程
    $assert.assertTrue($threads.currentThread() != $threads.mainThread(), "当前线程不是主线程")
    // 断言当前线程不是主线程
    for (i in 0..<10) {
        $console.log("子线程->$i")
        // 当前线程睡眠100毫秒
        $threads.sleep(100)
    }
}
// 断言当前线程为主线程
$assert.assertTrue($threads.currentThread() == $threads.mainThread(), "当前线程为主线程")
// 主线程睡眠300毫秒,子线程会输出3次(0-2)
$threads.sleep(300)
// 停止子线程
$threads.stopThread(scriptThread)
```
