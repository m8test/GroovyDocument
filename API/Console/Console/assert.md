功能:

+ 如果断言为 false,则将一个错误消息写入控制台.如果断言是 true,没有任何反应.注意:
  与 [Assert.assertTrue()](/API/Assert/Assert/README.md?id=assertTrue)
  不同,此处即使断言为false也不会导致线程退出,只会在控制台打印信息而已.

定义:

+ [Console](/API/Console/Console/README.md) assert(boolean assertion, Object message, Object...
  otherMessages)

参数:

+ boolean assertion - 一个布尔表达式.如果 assertion 为假,消息将会被输出到控制台之中.
+ Object message - 需要输出到控制台的消息.
+ Object... otherMessages - 如果还要输出多个对象,可以在后面添加任意数量的对象.

返回值:

+ [Console](/API/Console/Console/README.md) - 返回调用对象本身,方便链式调用.

示例代码:

+ 分别断言 1 == 2 和 2 == 2 ,其中前者会输出信息到控制台,后者则不会.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 输出等级为assert的信息,由于表达式 1 == 2 为false,所以会输出内容
$console.assert(1 == 2, "assert 1 == 2")
// 输出等级为assert的信息,由于表达式 2 == 2 为true,所以不会输出内容
$console.assert(2 == 2, "assert 2 == 2")
```