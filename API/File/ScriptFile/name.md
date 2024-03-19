功能:

+ 获取文件名,包含扩展名,如果不需要扩展名请使用
  [ScriptFile.nameWithoutExtension()](/API/File/ScriptFile/README.md?id=nameWithoutExtension)

定义:

+ String name()

参数:

+ 无

返回值:

+ String - 文件名,包含扩展名

示例代码:

+ 通过 [ScriptFile.name()](/API/File/ScriptFile/README.md?id=name) 获取文件名.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_name.txt')
}
// ScriptFile.name() 用于获取文件名
$assert.assertTrue(scriptFile.name() == "test_name.txt", "文件名")
```