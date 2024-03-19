功能:

+ 向文件中写入字节数据.

定义:

+ [ScriptFile](/API/File/ScriptFile/README.md) writeBytes(byte[] bytes)

参数:

+ byte[] bytes - 要写入文件中的字节数据.

返回值:

+ [ScriptFile](/API/File/ScriptFile/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [ScriptFile.writeBytes()](/API/File/ScriptFile/README.md?id=writeBytes) 向文件中写入字节数据.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_writeBytes.txt')
}
// ScriptFile.writeBytes() 用于向文件中添加字节数据,会清空文件中的数据
scriptFile.writeBytes($strings.toBytes("writeBytes"))
// ScriptFile.readText() 用于读取文件内容为文本内容
def text = scriptFile.readText()
$assert.assertTrue(text == "writeBytes", "文件内容")
```