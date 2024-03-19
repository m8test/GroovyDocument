功能:

+ 按行读取文件内容,读取文件全部内容后返回.

定义:

+ List\<String\> readLines(String charset = "UTF-8")

参数:

+ String charset - 字符编码

返回值:

+ List\<String\> - 文件中所有的行

示例代码:

+ 通过 [ScriptFile.readLines()](/API/File/ScriptFile/README.md?id=readLines) 按行读取文件所有内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_readLines.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText("line1\nline2")
// ScriptFile.readLines() 用于按行读取文件内容
def lines = scriptFile.readLines("UTF-8")
$assert.assertTrue(lines[0] == "line1", "line1")
$assert.assertTrue(lines[1] == "line2", "line2")

```