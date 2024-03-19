```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 开启一个子线程不指定线程名
$threads.startThread {
    // 断言当前线程不是主线程
    $assert.assertTrue($threads.currentThread() != $threads.mainThread(), "当前线程不是主线程")
    // 打印当前脚本名字
    $console.log($threads.currentThread().name())
}
// 开启第2个子线程并指定线程名
$threads.startThread({
    // 断言当前线程不是主线程
    $assert.assertTrue($threads.currentThread() != $threads.mainThread())
    // 打印当前线程名字
    $console.log($threads.currentThread().name())
}, "自定义子线程名")
// 断言当前线程为主线程
$assert.assertTrue($threads.currentThread() == $threads.mainThread(), "当前线程为主线程")
```