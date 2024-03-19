功能:

+ 判断线程是否存活.

定义:

+ boolean isAlive()

参数:

+ 无

返回值:

+ boolean
    + true 线程还在运行
    + false 线程已经结束运行

示例代码:

+ 开启一个子线程每隔100毫秒打印一次,共打印5次.在主线程中休眠200毫秒后断言子线程存活,再睡眠500毫秒断言子线程结束.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 开启一个子线程不指定线程名
def childThread = $threads.startThread {
    // 断言当前线程不是主线程
    $assert.assertTrue($threads.currentThread() != $threads.mainThread(), "当前线程不是主线程")
    // 每隔100毫秒打印一次
    for (i in 0..<5) {
        $console.log("子线程->$i")
        $threads.sleep(100)
    }
}
// 主线程睡眠200毫秒
$threads.sleep(200)
// 断言子线程存活
$assert.assertTrue(childThread.isAlive(), "子线程正在运行...")
// 再睡眠500毫秒
$threads.sleep(500)
// 断言子线程不存活(结束)
$assert.assertFalse(childThread.isAlive(), "子线程结束.")
```