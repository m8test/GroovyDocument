功能:

+ 启动一个新线程.

定义:

+ [ScriptThread](/API/Thread/ScriptThread/README.md) startThread(Closure runnable, String name)

参数:

+ Closure runnable - 线程执行的内容
    + 参数 - 无
    + delegate - 无
+ String name - 线程名,默认为`ScriptThread-${id}`,id为数字,默认情况下会自动增长.

返回值:

+ [ScriptThread](/API/Thread/ScriptThread/README.md) - 新建的脚本线程对象

示例代码:

+ 启动两个子线程打印输出线程名,其中一个不指定线程名,另外一个不指定线程名.

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