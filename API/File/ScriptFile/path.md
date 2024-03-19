功能:

+ 获取文件路径

定义:

+ String path()

参数:

+ 无

返回值:

+ String - 文件路径

示例代码:

+ 通过 [ScriptFile.path()](/API/File/ScriptFile/README.md?id=path) 获取文件路径.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_path.txt')
}
// ScriptFile.path() 用于获取文件路径
def path = scriptFile.path()
$assert.assertTrue(path == "/sdcard/test_path.txt", "文件路径")
```