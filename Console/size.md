```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 设置控制台最多只显示5条日志
$console.size(5)
// 打印当前日志容量,结果为5
$console.log("日志容量为:" + $console.size())
// 输出10条日志,每个300毫秒输出一条日志,如果当前日志超过5,最早输出的日志会自动被删除
for (i in 0..<10) {
    $console.log(i)
    $threads.sleep(300)
}
```