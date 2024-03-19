功能:

+ 重置计数器,此函数有一个可选参数 label .
+ 如果提供了参数 label ,此函数会重置与 label 关联的计数器.
+ 如果省略了参数 label ,此函数会重置默认的计数器.

定义:

+ [Console](/API/Console/Console/README.md) countReset(String label = "default")

参数:

+ String label
    + 若传入此参数 [Console.countReset()](/API/Console/Console/README.md?id=countReset) 重置此 label
      的对应的计数器为0.
    + 若忽略此参数 [Console.countReset()](/API/Console/Console/README.md?id=countReset) 重置默认的计数器(default)
      为0.

返回值:

+ [Console](/API/Console/Console/README.md) - 返回调用对象本身,方便链式调用.

示例代码:

+ 不设置和设置label分别调用两次 [Console.count()](/API/Console/Console/README.md?id=count)
  后重置计数器再分别调用两次 [Console.count()](/API/Console/Console/README.md?id=count) .

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 忽略label,此处为1
$console.count()
// 忽略label,此处为2
$console.count()
// 重置默认计数器
$console.countReset()
// 忽略label,此处为1
$console.count()
// 忽略label,此处为2
$console.count()
// 计数器label
def label = "label"
// 设置label,此处为1
$console.count(label)
// 设置label,此处为2
$console.count(label)
// 重置label对应的计数器
$console.countReset(label)
// 设置label,此处为1
$console.count(label)
// 设置label,此处为2
$console.count(label)
```
