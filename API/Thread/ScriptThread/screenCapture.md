功能:

+ 获取线程对应的屏幕截图器.只有通过
  [Threads.startThread()](/API/Thread/Threads/README.md?id=startThread)
  启动的线程以及脚本主线程(不是安卓主线程)
  才会有屏幕截图器,如果是其他线程调用此方法返回结果为空

定义:

+ [ScreenCapture](/API/Image/ScreenCapture/README.md) screenCapture()

参数:

+ 无

返回值:

+ [ScreenCapture](/API/Image/ScreenCapture/README.md) - 线程对应的屏幕截图器.

示例代码:

+ 通过 [ScriptThread.screenCapture()](/API/Thread/ScriptThread/README.md?id=screenCapture)
  方法获取线程对应的屏幕截图器.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 获取主线程
def mainThread = $threads.mainThread()
// ScriptThread.screenCapture() 用于获取线程对应的屏幕截图器
def screenCapture = mainThread.screenCapture()
// ScreenCapture.requestPermission() 用于获取截屏权限
def hasPermission = screenCapture.hasPermission()
if (hasPermission) {
    // ScreenCapture.captureScreen() 用于截取屏幕
    def screenImage = screenCapture.captureScreen()
    // Images.clip() 用于裁剪图片
    def clipImage = $images.clip(screenImage, {
        // delegate -> Rect
        // Rect.left() 用于设置矩形的左边缘相对于 x 轴的偏移量。
        left(100)
        // Rect.right() 用于设置矩形的右边缘相对于 x 轴的偏移量。
        right(200)
        // Rect.top() 用于设置矩形的底边距 y 轴的偏移量。
        top(100)
        // Rect.bottom() 用于设置矩形的上边缘相对于 y 轴的偏移量。
        bottom(200)
    })
    // Images.matchTemplate() 用于匹配模板
    def matchingResults = $images.matchTemplate {
        // delegate -> TemplateMatcher
        // TemplateMatcher.image() 用于设置原图(大图)
        image(screenImage)
        // TemplateMatcher.template() 用于设置模板图(小图)
        template(clipImage)
    }
    $console.log(matchingResults)
} else {
    $console.error("没有截取权限")
}
```