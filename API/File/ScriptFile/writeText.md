功能:

+ 向文件中写入文本内容.

定义:

+ [ScriptFile](/API/File/ScriptFile/README.md) writeText(String text, String charset = "UTF-8")

参数:

+ String text - 需要写入文件的内容
+ String charset - 字符编码

返回值:

+ String - 文件中的文本内容

示例代码:

+ 通过 [ScriptFile.writeText()](/API/File/ScriptFile/README.md?id=writeText) 向文件中写入文本内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_writeText.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText("writeText", "UTF-8")
// ScriptFile.readText() 用于读取文件内容为文本内容
def text = scriptFile.readText()
$assert.assertTrue(text == "writeText", "文件内容")
```