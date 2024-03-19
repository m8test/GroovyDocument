功能:

+ 删除文件/空文件夹,如果需要删除文件夹及其所有子文件和子文件夹请使用
  [ScriptFile.deleteRecursively()](/API/File/ScriptFile/README.md?id=deleteRecursively)

定义:

+ boolean delete()

参数:

+ 无

返回值:

+ boolean - 如果删除文件/空文件夹成功返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.delete()](/API/File/ScriptFile/README.md?id=delete) 删除文件.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象,源文件
def scriptFile = $files.buildFile {
  // delegate -> FileBuilder
  // FileBuilder.path() 用于设置文件路径
  path('/sdcard/', 'test_delete.txt')
}
// ScriptFile.createFile() 用于创建文件
scriptFile.createFile()
// ScriptFile.delete() 用于删除本地文件
$assert.assertTrue(scriptFile.delete(), "删除文件")
// 断言文件不存在
$assert.assertFalse(scriptFile.exists(), "文件不存在")
```