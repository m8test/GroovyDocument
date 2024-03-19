功能:

+ 跳转到无障碍服务设置页面,如果无障碍服务已经启动则无任何操作

定义:

+ [Accessibility](/API/Accessibility/Accessibility/README.md) enable()

参数:

+ 无

返回值:

+ [Accessibility](/API/Accessibility/Accessibility/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [Accessibility.enable()](/API/Accessibility/Accessibility/README.md?id=enable) 方法跳转到无障碍服务设置页面

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