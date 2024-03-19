功能:

+ 判断系统是否开启开发者选项

定义:

+ boolean isDevelopmentSettingsEnabled()

参数:

+ 无

返回值:

+ boolean - 如果系统已经开启开发者选项返回true,否则返回false

示例代码:

+ 通过
  [System.isDevelopmentSettingsEnabled()](/API/Device/System/README.md?id=isDevelopmentSettingsEnabled)
  判断系统是否开启开发者选项.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Device.system() 用于获取System对象
def system = $device.system()
// System.isDevelopmentSettingsEnabled() 用于判断系统是否开启开发者选项
$console.log("系统是否开启开发者选项", system.isDevelopmentSettingsEnabled())
```