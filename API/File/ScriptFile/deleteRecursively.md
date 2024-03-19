功能:

+ 删除文件或者文件夹(文件夹以及其中所有内容都会被删除)

定义:

+ boolean deleteRecursively()

参数:

+ 无

返回值:

+ boolean - 如果删除文件/文件夹成功返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.deleteRecursively()](/API/File/ScriptFile/README.md?id=deleteRecursively) 删除文件夹.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_deleteRecursively')
}
// ScriptFile.mkdirs() 用于递归创建目录
scriptFile.mkdirs()
// Files.buildFile() 用于构建一个 ScriptFile 对象,这是一个子目录
def subDir = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path(scriptFile.path(), "dir")
}
// ScriptFile.mkdirs() 用于递归创建目录
subDir.mkdirs()
// Files.buildFile() 用于构建一个 ScriptFile 对象,子目录下的文件
def subDirContent = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path(subDir.path(), "subDir.txt")
}
// ScriptFile.writeText() 用于向文件中写入文本数据
subDirContent.writeText("subDir")
// Files.buildFile() 用于构建一个 ScriptFile 对象,源目录根目录下的文件
def content = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path(scriptFile.path(), "content.txt")
}
// ScriptFile.writeText() 用于向文件中写入文本数据
content.writeText("content")
// ScriptFile.deleteRecursively() 用于删除文件夹及其子文件/文件夹
$assert.assertTrue(scriptFile.deleteRecursively(), "删除文件夹")
```