功能:

+ 向控制台输出一条警告信息.

定义:

+ [Console](/API/Console/Console/README.md) warn(Object data, Object... options)

参数:

+ Object data - 需要输出到控制台的数据
+ Object... options - 额外需要输出到控制台的数据

返回值:

+ [Console](/API/Console/Console/README.md) - 返回调用对象本身,方便链式调用.

实例代码:

+ 向控制台输出一条警告信息.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 输出等级为warn的信息
$console.warn("warn")
```
