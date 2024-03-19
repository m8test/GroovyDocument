功能:

+ 新建文件到本地.

定义:

+ boolean createFile()

参数:

+ 无

返回值:

+ boolean - 如果创建文件成功返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.createFile()](/API/File/ScriptFile/README.md?id=createFile) 创建文件.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象,源文件
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_createFile.txt')
}
// ScriptFile.exists() 用于判断文件是否存在
if (scriptFile.exists()) {
    // ScriptFile.delete() 用于删除本地文件
    scriptFile.delete()
}
// 断言文件不存在
$assert.assertFalse(scriptFile.exists(), "文件不存在")
// ScriptFile.createFile() 用于创建文件
scriptFile.createFile()
// 断言文件存在
$assert.assertTrue(scriptFile.exists(), "文件存在")
```