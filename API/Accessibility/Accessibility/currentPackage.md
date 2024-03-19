功能:

+ 获取当前应用包名

定义:

+ String currentPackage()

参数:

+ 无

返回值:

+ String - 当前应用包名

示例代码:

+ 启动一个Activity,
  并通过 [Accessibility.currentPackage()](/API/Accessibility/Accessibility/README.md?id=currentPackage)
  方法获取当前应用包名

```groovy
// Accessibility.currentPackage() 用于获取当前应用包名
def packageName = $accessibility.currentPackage()
$console.log(packageName)
```