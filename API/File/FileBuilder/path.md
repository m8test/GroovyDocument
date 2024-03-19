功能:

+ 设置文件路径,默认会在外部空间中的应用私有目录([Files.externalFilesDir()](/API/File/Files/README.md?id=externalFilesDir))
  中创建,如果想在其他地方创建文件,可以通过 [FileBuilder.absolutePath()](/API/File/FileBuilder/README.md?id=absolutePath)
  实现

定义:

+ [FileBuilder](/API/File/FileBuilder/README.md) path(String parent, String child = null)

参数:

+ String parent - 父路径
+ String child - 子路径

返回值:

+ [FileBuilder](/API/File/FileBuilder/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [FileBuilder.path()](/API/File/FileBuilder/README.md?id=path) 设置文件路径

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_path.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText('path')
// 断言文件内容
$assert.assertTrue(scriptFile.readText() == 'path', "test_path.txt文件内容")
```