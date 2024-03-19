功能:

+ 获取文件扩展名,例如 a.txt 返回 txt, b.groovy 返回 groovy

定义:

+ String extension()

参数:

+ 无

返回值:

+ String - 文件扩展名

示例代码:

+ 通过 [ScriptFile.extension()](/API/File/ScriptFile/README.md?id=extension) 获取文件扩展名.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_extension.txt')
}
// ScriptFile.extension() 用于获取文件扩展名
$assert.assertTrue(scriptFile.extension() == "txt", "文件扩展名")
```