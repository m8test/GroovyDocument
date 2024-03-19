功能:

+ 向文件中添加文本内容.

定义:

+ [ScriptFile](/API/File/ScriptFile/README.md) appendText(String text, String charset = "UTF-8")

参数:

+ String text - 需要添加到文件中的文本内容.
+ String charset - 字符编码

返回值:

+ [ScriptFile](/API/File/ScriptFile/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [ScriptFile.appendText()](/API/File/ScriptFile/README.md?id=appendText) 向文件中添加文本内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_appendText.txt')
}
// ScriptFile.writeText() 用于向文件中添加文本内容,会清空文件中的数据
scriptFile.writeText("appendText1", "UTF-8")
// ScriptFile.appendText() 用于向文件中添加文本内容
scriptFile.appendText("appendText2", "UTF-8")
// ScriptFile.readText() 用于读取文件内容为文本内容
def text = scriptFile.readText()
$assert.assertTrue(text == "appendText1appendText2", "文件内容")
```