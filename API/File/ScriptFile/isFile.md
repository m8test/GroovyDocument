功能:

+ 判断该文件是否为文件类型.

定义:

+ boolean isFile()

参数:

+ 无

返回值:

+ boolean - 如果该文件是文件类型返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.isFile()](/API/File/ScriptFile/README.md?id=isFile) 判断文件是否为文件类型.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_isFile.txt')
}
// ScriptFile.createFile() 用于创建文件
scriptFile.createFile()
// ScriptFile.isFile() 用于判断文件是否为文件类型
$assert.assertTrue(scriptFile.isFile(), "文件是文件类型")
```