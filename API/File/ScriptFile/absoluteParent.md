功能:

+ 获取文件父目录绝对路径

定义:

+ String absoluteParent()

参数:

+ 无

返回值:

+ String - 文件父目录绝对路径

示例代码:

+ 通过 [ScriptFile.absoluteParent()](/API/File/ScriptFile/README.md?id=absoluteParent) 获取文件父目录绝对路径.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_absoluteParent.txt')
}
// ScriptFile.absoluteParent() 用于获取文件父目录绝对路径
def absoluteParent = scriptFile.absoluteParent()
// Files.externalFilesDir() 用于获取外部空间中的应用私有目录
def sdcardPath = $files.externalFilesDir("sdcard")
$assert.assertTrue(absoluteParent == sdcardPath, "文件父目录绝对路径")
```