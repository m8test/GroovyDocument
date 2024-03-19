功能:

+ 获取文件绝对路径

定义:

+ String absolutePath()

参数:

+ 无

返回值:

+ String - 文件绝对路径

示例代码:

+ 通过 [ScriptFile.absolutePath()](/API/File/ScriptFile/README.md?id=absolutePath) 获取文件绝对路径.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_absolutePath.txt')
}
// ScriptFile.absolutePath() 用于获取文件绝对路径
def absolutePath = scriptFile.absolutePath()
// Files.externalFilesDir() 用于获取外部空间中的应用私有目录
def sdcardPath = $files.externalFilesDir("sdcard")
$assert.assertTrue(absolutePath == "${sdcardPath}/test_absolutePath.txt", "文件绝对路径")
```