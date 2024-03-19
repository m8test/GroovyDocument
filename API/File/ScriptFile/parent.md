功能:

+ 获取文件父目录路径.例如 /sdcard/1.txt 的 parent 为 /sdcard

定义:

+ String parent()

参数:

+ 无

返回值:

+ String - 文件父目录路径

示例代码:

+ 通过 [ScriptFile.parent()](/API/File/ScriptFile/README.md?id=parent) 获取文件父目录路径.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_parent.txt')
}
// ScriptFile.parent() 用于获取文件父目录路径
$assert.assertTrue(scriptFile.parent() == "/sdcard", "文件父目录")
```