功能:

+ 遍历文本文件中每一行.

定义:

+ [ScriptFile](/API/File/ScriptFile/README.md) forEachLine(String charset = "UTF-8", Closure
  closure)

参数:

+ String charset - 字符编码,默认为 UTF-8
+ Closure closure - 每读取一行文本内容都会调用闭包
    + 参数
        + String line - 读取到的行内容
    + delegate - 无

返回值:

+ [ScriptFile](/API/File/ScriptFile/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [ScriptFile.forEachLine()](/API/File/ScriptFile/README.md?id=forEachLine) 按行读取文件中的内容

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_forEachLine.txt')
}
// ScriptFile.writeText() 用于向文件中添加文本内容,会清空文件中的数据
scriptFile.writeText("line1\nline2\nline3")
// ScriptFile.forEachLine() 用于按行读取文件内容
scriptFile.forEachLine("UTF-8") {
    // 分别输出 line1 line2 line3
    $console.log(it)
}
```