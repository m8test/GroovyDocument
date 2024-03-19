功能:

+ 读取文件为字节数组.

定义:

+ byte[] readBytes()

参数:

+ 无

返回值:

+ byte[] - 文件中的字节内容

示例代码:

+ 通过 [ScriptFile.readBytes()](/API/File/ScriptFile/README.md?id=readBytes) 读取文件为字节数组.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_readBytes.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText("readBytes")
// ScriptFile.readBytes() 用于读取文件内容为字节数组
def bytes = scriptFile.readBytes()
$assert.assertTrue($strings.fromBytes(bytes) == "readBytes", "文件内容")
```