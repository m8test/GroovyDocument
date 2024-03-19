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