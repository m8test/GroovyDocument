功能:

+ 获取外部空间中的应用私有目录

定义:

+ String externalFilesDir(String type)

参数:

+ String type - 子目录

返回值:

+ String - 外部空间中的应用私有目录

示例代码:

+ 通过 [Files.externalFilesDir()](/API/File/Files/README.md?id=externalFilesDir) 获取外部空间中的应用私有目录

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.externalFilesDir() 用于获取外部空间中的应用私有目录
$console.log($files.externalFilesDir("type"))
```