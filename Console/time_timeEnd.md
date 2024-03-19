```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
def label = "label"
// 开启一个计时器
$console.time(label)
// 模拟耗时操作
for (i in 0..<10) {
    $threads.sleep(100)
}
// 结束计时器
$console.timeEnd(label)
```