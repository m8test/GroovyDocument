功能:

+ 读取文件为文本.

定义:

+ String readText(String charset = "UTF-8")

参数:

+ String charset - 字符编码,默认为 UTF-8

返回值:

+ String - 文件中的文本内容

示例代码:

+ 通过 [ScriptFile.readText()](/API/File/ScriptFile/README.md?id=readText) 读取文件为文本.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_readText.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText("readText")
// ScriptFile.readText() 用于读取文件内容为文本内容
def text = scriptFile.readText("UTF-8")
$assert.assertTrue(text == "readText", "文件内容")
```