功能:

+ 向文件中添加字节数据.

定义:

+ [ScriptFile](/API/File/ScriptFile/README.md) appendBytes(byte[] bytes)

参数:

+ byte[] bytes - 需要添加到文件中的字节内容.

返回值:

+ [ScriptFile](/API/File/ScriptFile/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [ScriptFile.appendBytes()](/API/File/ScriptFile/README.md?id=appendBytes) 向文件中添加字节数据.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_appendBytes.txt')
}
// ScriptFile.writeBytes() 用于向文件中添加字节数据,会清空文件中的数据
scriptFile.writeBytes($strings.toBytes("appendBytes1"))
// ScriptFile.appendBytes() 用于向文件中添加字节数据
scriptFile.appendBytes($strings.toBytes("appendBytes2"))
// ScriptFile.readBytes() 用于读取文件内容为字节数组
def bytes = scriptFile.readBytes()
$assert.assertTrue($strings.fromBytes(bytes) == "appendBytes1appendBytes2", "文件内容")
```