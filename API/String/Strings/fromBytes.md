功能:

+ 将字节数组转为字符串

定义:

+ String fromBytes(byte[] bytes, String charset = "UTF-8")

参数:

+ byte[] bytes - 需要转成字符串的字节数组.
+ String charset - 字符编码

返回值:

+ String - 字节数组对应的字符串

示例代码:

+ 通过 [Strings.fromBytes()](/API/String/Strings/README.md?id=fromBytes) 将字节数组转成字符串.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Strings.toBytes() 用于将字符串转成字节数组
def bytes = $strings.toBytes("fromBytes", "UTF-8")
// Strings.fromBytes() 用于将字节数组转成字符串
def text = $strings.fromBytes(bytes, "UTF-8")
// 断言结果
$assert.assertTrue(text == "fromBytes", "转换结果")****
```