功能:

+ 判断本地是否存在该文件/文件夹.

定义:

+ boolean exists()

参数:

+ 无

返回值:

+ boolean - 如果文件/文件夹存在返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.exists()](/API/File/ScriptFile/README.md?id=exists) 判断文件夹/文件是否存在.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_exists.txt')
}
// ScriptFile.createFile() 用于创建文件
scriptFile.createFile()
// ScriptFile.exists() 用于判断文件是否存在
$assert.assertTrue(scriptFile.exists(), "文件存在")
// ScriptFile.delete() 用于删除本地文件
$assert.assertTrue(scriptFile.delete(), "删除文件")
// ScriptFile.exists() 用于判断文件是否存在
$assert.assertFalse(scriptFile.exists(), "文件不存在")
```