功能:

+ 将此文件及其所有子文件复制到指定的目标路径。
    + 如果在到达目的地的途中丢失了一些目录，则将创建这些目录。
    + 如果此文件路径指向单个文件，则它将被复制到具有路径目标的文件。如果此文件路径指向某个目录，则其子目录将被复制到具有路径目标的目录。
    + 如果目标已经存在，当覆盖参数允许时，将在复制之前删除该目标。
    + 该操作不保留复制的文件属性，如创建/修改日期、权限等。

定义:

+ boolean copyRecursively([ScriptFile](/API/File/ScriptFile/README.md) dest, boolean override)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) dest - 目标文件
+ boolean override - 如果目标文件存在是否覆盖

返回值:

+ boolean - 如果复制成功返回true,否则返回false

示例代码:

+ 通过 [ScriptFile.copyRecursively()](/API/File/ScriptFile/README.md?id=copyRecursively)
  复制文件夹以及其所有子文件/子文件夹.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Files.buildFile() 用于构建一个 ScriptFile 对象,源文件
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path('/sdcard/', 'test_copyRecursively')
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
// Files.buildFile() 用于构建一个 ScriptFile 对象,目的文件
def dest = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path("/sdcard/", "test_copyRecursively_bak")
}
// ScriptFile.copyRecursively() 用于将此文件及其所有子文件复制到指定的目标路径。
scriptFile.copyRecursively(dest, true)
```