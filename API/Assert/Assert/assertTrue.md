功能:

+ 断言条件为真,如果条件为假则抛出 AssertionError,否则没有任何反应.

定义:

+ [Assert](/API/Assert/Assert/README.md) assertTrue(boolean assertion, Object... message)

参数:

+ boolean assertion - 断言的条件,如果条件为假则抛出 AssertionError,否则没有任何反应.
+ Object... message - 可变参数,抛出异常时以此参数作为错误信息.

返回值:

+ [Assert](/API/Assert/Assert/README.md) - 如果断言条件为真,则返回对象本身,方便链式调用.

示例代码:

+ 断言当前线程为主线程.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 断言当前线程不是主线程
$assert.assertTrue($threads.currentThread() == $threads.mainThread(), "断言 \$threads.currentThread() == \$threads.mainThread() 为真")
```