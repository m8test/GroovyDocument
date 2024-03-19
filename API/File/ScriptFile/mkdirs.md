功能:

+ 递归创建文件夹.

定义:

+ boolean mkdirs()

参数:

+ 无

返回值:

+ boolean - 如果创建成功返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.mkdirs()](/API/File/ScriptFile/README.md?id=mkdirs) 创建文件夹.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_mkdirs')
}
// ScriptFile.exists() 用于判断文件是否存在
if (scriptFile.exists()) {
    // ScriptFile.delete() 用于删除本地文件
    scriptFile.delete()
}
// ScriptFile.mkdirs() 用于递归创建目录
$assert.assertTrue(scriptFile.mkdirs(), "创建文件夹")
```