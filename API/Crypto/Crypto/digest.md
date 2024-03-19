功能:

+ 获取数据摘要(不可逆加密).

定义:

+ String digest(String algorithm, byte[] data)

参数:

+ String algorithm - 摘要算法,例如 MD5,SHA1,SHA224,SHA256,SHA384,SHA512
+ byte[] data - 需要获取摘要的二进制数据

返回值:

+ String - 摘要信息

示例代码:

+ 通过 [Crypto.digest()](/API/Crypto/Crypto/README.md?id=digest) 获取数据摘要.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()

// MD5 加解密例子
// Strings.toBytes() 用于将字符串转成字节数组
def data = $strings.toBytes('MD5')
// Crypto.digest() 用于获取数据摘要
def digest = $crypto.digest('MD5', data)
$console.log(digest)

//// SHA1 加解密例子
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('SHA1')
//// Crypto.digest() 用于获取数据摘要
//def digest = $crypto.digest('SHA1', data)
//$console.log(digest)

//// SHA224 加解密例子
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('SHA224')
//// Crypto.digest() 用于获取数据摘要
//def digest = $crypto.digest('SHA224', data)
//$console.log(digest)

//// SHA256 加解密例子
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('SHA256')
//// Crypto.digest() 用于获取数据摘要
//def digest = $crypto.digest('SHA256', data)
//$console.log(digest)


//// SHA384 加解密例子
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('SHA384')
//// Crypto.digest() 用于获取数据摘要
//def digest = $crypto.digest('SHA384', data)
//$console.log(digest)

//// SHA512 加解密例子
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('SHA512')
//// Crypto.digest() 用于获取数据摘要
//def digest = $crypto.digest('SHA512', data)
//$console.log(digest)
```