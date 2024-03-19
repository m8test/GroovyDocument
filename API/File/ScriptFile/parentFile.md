功能:

+ 获取文件父目录 [ScriptFile](/API/File/ScriptFile/README.md) 对象.

定义:

+ [ScriptFile](/API/File/ScriptFile/README.md) parentFile()

参数:

+ 无

返回值:

+ [ScriptFile](/API/File/ScriptFile/README.md) - 文件父目录对象

示例代码:

+ 通过 [ScriptFile.parentFile()](/API/File/ScriptFile/README.md?id=parentFile) 获取文件父目录对象.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_parentFile.txt')
}
// ScriptFile.parentFile() 用于获取文件父目录对象
def parentFile = scriptFile.parentFile()
$assert.assertTrue(parentFile.path() == "/sdcard", "文件父目录")
```