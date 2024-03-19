功能:

+ 重命名文件.

定义:

+ boolean renameTo([ScriptFile](/API/File/ScriptFile/README.md) dest)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) dest - 重命名的后的
  [ScriptFile](/API/File/ScriptFile/README.md) 对象

返回值:

+ boolean - 如果重命名成功返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.renameTo()](/API/File/ScriptFile/README.md?id=renameTo) 重命名文件.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_renameTo_before.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText("renameTo")
// Files.buildFile() 用于构建一个 ScriptFile 对象
def dest = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_renameTo_after.txt')
}
// ScriptFile.renameTo() 用于重命名文件
scriptFile.renameTo(dest)
$assert.assertTrue(dest.readText() == "renameTo", "重命名文件后的内容")
```