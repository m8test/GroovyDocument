功能:

+ 断言条件为假,如果条件为真则抛出 AssertionError,否则没有任何反应.

定义:

+ [Assert](/API/Assert/Assert/README.md) assertFalse(boolean assertion, Object... message)

参数:

+ boolean assertion - 断言的条件,如果条件为真则抛出 AssertionError,否则没有任何反应.
+ Object... message - 可变参数,抛出异常时以此参数作为错误信息.

返回值:

+ [Assert](/API/Assert/Assert/README.md) - 如果断言条件为假,则返回对象本身,方便链式调用.

示例代码:

+ 开启一个子线程并在其中断言该线程不是主线程.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 开启一个子线程
$threads.startThread {
    // 断言当前线程不是主线程
    $assert.assertFalse($threads.currentThread() == $threads.mainThread(), "断言 \$threads.currentThread() == \$threads.mainThread() 为假")
}
```