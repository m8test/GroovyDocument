功能:

+ 获取文件名,不包含扩展名

定义:

+ String nameWithoutExtension()

参数:

+ 无

返回值:

+ String - 文件名,不包含扩展名

示例代码:

+ 通过 [ScriptFile.nameWithoutExtension()](/API/File/ScriptFile/README.md?id=nameWithoutExtension)
  获取文件名(不包含扩展名).

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_nameWithoutExtension.txt')
}
// ScriptFile.nameWithoutExtension() 用于获取文件名(不包含扩展名)
$assert.assertTrue(scriptFile.nameWithoutExtension() == "test_nameWithoutExtension", "文件名(不包含扩展名)")
```