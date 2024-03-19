功能:

+ 压缩文件

定义:

+ boolean zipFile([ScriptFile](/API/File/ScriptFile/README.md)
  src, [ScriptFile](/API/File/ScriptFile/README.md) dest, String comment = null)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) src - 需要被压缩的文件或者文件夹
+ [ScriptFile](/API/File/ScriptFile/README.md) dest - 压缩后的文件
+ String comment - comment字段

返回值:

+ boolean - 如果压缩成功返回true,否则返回false

示例代码:

+ 通过 [Files.zipFile()](/API/File/Files/README.md?id=zipFile) 压缩文件.

```groovy
package sample.文件.Files

/*
功能:
+ 压缩文件

定义:
+ boolean zipFile(ScriptFile src, ScriptFile dest, String comment = null)

参数:
+ ScriptFile src - 需要被压缩的文件或者文件夹
+ ScriptFile dest - 压缩后的文件
+ String comment - comment字段

返回值:
+ boolean - 如果压缩成功返回true,否则返回false

示例代码:
+ 通过 Files.zipFile() 压缩文件.
 */
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_zipFile.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText('zipFile')
// 断言文件内容
$assert.assertTrue(scriptFile.readText() == 'zipFile', "test_zipFile.txt文件内容")
// Files.buildFile() 用于构建一个 ScriptFile 对象
def dest = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path("/sdcard/test_zipFile.zip")
}
// Files.zipFile() 用于压缩文件
$assert.assertTrue($files.zipFile(scriptFile, dest, "This is comment"), "压缩文件")
```