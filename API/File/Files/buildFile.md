功能:

+ 构建一个 [ScriptFile](/API/File/ScriptFile/README.md) 对象.

定义:

+ [ScriptFile](/API/File/ScriptFile/README.md) buildFile(Closure closure)

参数:

+ Closure closure - 构建文件的闭包
    + 参数 - 无
    + delegate - [FileBuilder](/API/File/FileBuilder/README.md)

返回值:

+ [ScriptFile](/API/File/ScriptFile/README.md) - 新构建的 [ScriptFile](/API/File/ScriptFile/README.md)
  对象

示例代码:

+ 通过 [Files.buildFile()](/API/File/Files/README.md?id=buildFile)
  构建一个 [ScriptFile](/API/File/ScriptFile/README.md) 对象并向其中写入文本内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_buildFile.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText('buildFile')
// 断言文件内容
$assert.assertTrue(scriptFile.readText() == 'buildFile', "test_buildFile.txt文件内容")
```