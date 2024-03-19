```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 输出等级为verbose的信息
$console.verbose("verbose")
// 输出等级为debug的信息
$console.log("log")
// 输出等级为info的信息
$console.info("info")
// 输出等级为warn的信息
$console.warn("warn")
// 输出等级为error的信息
$console.error("error")
// 输出等级为assert的信息
$console.assert(1 == 2, "assert 1 == 2")
// 睡眠1秒钟后清空控制台
$threads.sleep(1000)
// 清空控制台输出内容
$console.clear()
```