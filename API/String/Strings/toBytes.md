功能:

+ 将字符串转成字节数组.

定义:

+ byte[] toBytes(String text, String charset = "UTF-8")

参数:

+ String text - 需要转成字节数组的字符串
+ String charset - 字符编码

返回值:

+ byte[] - 字符串转成字的字节数组

示例代码:

+ 通过 [Strings.toBytes()](/API/String/Strings/README.md?id=toBytes) 将字符串转成字节数组.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Strings.toBytes() 用于将字符串转成字节数组
def bytes = $strings.toBytes("toBytes", "UTF-8")
// Strings.fromBytes() 用于将字节数组转成字符串
def text = $strings.fromBytes(bytes, "UTF-8")
// 断言结果
$assert.assertTrue(text == "toBytes", "转换结果")
```