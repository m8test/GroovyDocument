功能:

+ 解压文件

定义:

+ List\<[ScriptFile](/API/File/ScriptFile/README.md)\>
  unzipFile([ScriptFile](/API/File/ScriptFile/README.md)
  src, [ScriptFile](/API/File/ScriptFile/README.md) dest, String password = null)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) src - 带解压的压缩包
+ [ScriptFile](/API/File/ScriptFile/README.md) dest - 解压后的路径
+ String password - 解压密码,默认为null

返回值:

+ List\<[ScriptFile](/API/File/ScriptFile/README.md)\> - 解压出来的压缩包中所有的文件

示例代码:

+ 通过 [Files.unzipFile()](/API/File/Files/README.md?id=unzipFile) 解压文件.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_unzipFile.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText('unzipFile')
// 断言文件内容
$assert.assertTrue(scriptFile.readText() == 'unzipFile', "test_unzipFile.txt文件内容")
// Files.buildFile() 用于构建一个 ScriptFile 对象
def zipFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path("/sdcard/test_unzipFile.zip")
}
// Files.zipFile() 用于压缩文件
$assert.assertTrue($files.zipFile(scriptFile, zipFile, "This is comment"), "压缩文件")
// Files.unzipFile() 用于解压文件
def filesInZipFile = $files.unzipFile(zipFile, $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path("/sdcard/test_unzipFile")
})
// 遍历所有文件
filesInZipFile.each {
    // 打印文件路径
    $console.log(it.path())
}
```