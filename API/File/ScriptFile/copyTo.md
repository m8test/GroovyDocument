功能:

+ 将此文件复制到给定的目标文件。
    + 如果在通往目标的途中缺少某些目录，则将创建这些目录。
    + 如果目标文件已经存在，除非override参数设置为true，否则此函数将失败。
    + 当覆盖为true且目标为目录时，仅当它为空时才替换它。
    + 如果此文件是一个目录，则复制时不包含其内容，即创建一个空的目标目录。
    + 如果要复制包括其内容的目录，请使用
      [ScriptFile.copyRecursively](/API/File/ScriptFile/README.md?id=copyRecursively) 。
      该操作不保留复制的文件属性，如创建/修改日期、权限等。

定义:

+ boolean copyTo([ScriptFile](/API/File/ScriptFile/README.md) dest, boolean override)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) dest - 目标文件
+ boolean override - 如果目标文件存在是否覆盖

返回值:

+ boolean - 如果复制成功返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.copyTo()](/API/File/ScriptFile/README.md?id=copyTo) 复制文件.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象,源文件
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_copyTo.txt')
}
// ScriptFile.writeText() 用于向文件中写入文本数据
scriptFile.writeText("copyTo")
// Files.buildFile() 用于构建一个 ScriptFile 对象,目标文件
def dest = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path("/sdcard/test_copyTo_bak.txt")
}
// ScriptFile.copyTo() 用于复制文件
def success = scriptFile.copyTo(dest, true)
$assert.assertTrue(success, "复制文件")
$assert.assertTrue(dest.readText() == "copyTo", "复制文件内容")
```