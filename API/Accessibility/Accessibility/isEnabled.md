功能:

+ 判断无障碍服务是否已经启动

定义:

+ boolean isEnabled()

参数:

+ 无

返回值:

+ boolean - 如果无障碍服务已经启动返回true,否则返回false

示例代码:

+ 通过 [Accessibility.isEnabled()](/API/Accessibility/Accessibility/README.md?id=isEnabled)
  方法判断无障碍服务是否已经启动

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Accessibility.isEnabled() 用于判断无障碍服务是否已经启动
def isEnabled = $accessibility.isEnabled()
if (!isEnabled) {
    // Accessibility.enable() 用于跳转到无障碍服务设置页面
    $accessibility.enable()
}
```