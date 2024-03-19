功能:

+ 判断该文件是否为文件夹.

定义:

+ boolean isDirectory()

参数:

+ 无

返回值:

+ boolean - 如果该文件是文件夹返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.isDirectory()](/API/File/ScriptFile/README.md?id=isDirectory) 判断文件是否为文件夹.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_isDirectory')
}
// ScriptFile.mkdirs() 用于递归创建目录
scriptFile.mkdirs()
// ScriptFile.isDirectory() 用于判断文件是否为文件夹
$assert.assertTrue(scriptFile.isDirectory(), "文件是文件夹")
```