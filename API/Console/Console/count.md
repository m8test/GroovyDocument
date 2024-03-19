功能:

+ 输出 [Console.count()](/API/Console/Console/README.md?id=count) 被调用的次数.此函数接受一个可选参数 label.
+ 如果有 label ,此函数输出为那个指定的 label 和 [Console.count()](/API/Console/Console/README.md?id=count) 被调用的次数.
+ 如果 label 被忽略, 此函数输出 [Console.count()](/API/Console/Console/README.md?id=count) 在其所处位置上被调用的次数.

定义:

+ int count(String label = "default")

参数:

+ String label - 字符串, 如果有, [Console.count()](/API/Console/Console/README.md?id=count) 输出此给定的 label
  及其被调用的次数.

返回值:

+ int - label 对应 [Console.count()](/API/Console/Console/README.md?id=count) 调用的次数.

示例代码:

+ 不设置label和设置两个不同的label分别调用两次 [Console.count()](/API/Console/Console/README.md?id=count) .

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 没有设置label,此处输出1
$console.count()
// 没有设置label,此处输出2
$console.count()
def label1 = "label1"
// 设置了label1,此处输出1
$console.count(label1)
// 设置了label1,此处输出2
$console.count(label1)
def label2 = "label2"
// 设置了label2,此处输出1
$console.count(label2)
// 设置了label2,此处输出2
$console.count(label2)
```