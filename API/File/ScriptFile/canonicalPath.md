功能:

+ 获取文件父目录规范路径

定义:

+ String canonicalPath()

参数:

+ 无

返回值:

+ String - 文件父目录规范路径

示例代码:

+ 通过 [ScriptFile.canonicalPath()](/API/File/ScriptFile/README.md?id=canonicalPath) 获取文件父目录规范路径.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_canonicalPath.txt')
}
// ScriptFile.canonicalPath() 用于获取文件父目录规范路径
def canonicalPath = scriptFile.canonicalPath()
// Files.externalFilesDir() 用于获取外部空间中的应用私有目录
def sdcardPath = $files.externalFilesDir("sdcard")
$assert.assertTrue(canonicalPath == sdcardPath, "文件父目录规范路径")
```