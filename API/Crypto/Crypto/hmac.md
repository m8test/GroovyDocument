功能:

+ 获取数据摘要(不可逆加密),HMAC为Hash-based Message Authentication Code缩写,意为密钥相关的哈希运算消息验证码.

定义:

+ String hmac(String algorithm, byte[] data, byte[] key)

参数:

+ String algorithm - 摘要算法,例如 HmacMD5,HmacSHA1,HmacSHA224,HmacSHA256,HmacSHA384,HmacSHA512
+ byte[] data - 需要获取摘要的二进制数据
+ byte[] key - 密钥

返回值:

+ String - 摘要信息

示例代码:

+ 通过 [Crypto.hmac()](/API/Crypto/Crypto/README.md?id=hmac) 获取数据摘要.

```groovy

// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()

//// HmacMD5 加解密例子
//// Crypto.newKey() 用于新建密钥
//def key = $crypto.newKey('HmacMD5', 512)
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('HmacMD5')
//// Crypto.hmac() 用于获取数据摘要
//def hmac = $crypto.hmac('HmacMD5', data, key.encoded())
//$console.log(hmac)

//// HmacSHA1 加解密例子
//// Crypto.newKey() 用于新建密钥
//def key = $crypto.newKey('HmacSHA1', 512)
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('HmacSHA1')
//// Crypto.hmac() 用于获取数据摘要
//def hmac = $crypto.hmac('HmacSHA1', data, key.encoded())
//$console.log(hmac)

//// HmacSHA224 加解密例子
//// Crypto.newKey() 用于新建密钥
//def key = $crypto.newKey('HmacSHA224', 512)
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('HmacSHA224')
//// Crypto.hmac() 用于获取数据摘要
//def hmac = $crypto.hmac('HmacSHA224', data, key.encoded())
//$console.log(hmac)


//// HmacSHA256 加解密例子
//// Crypto.newKey() 用于新建密钥
//def key = $crypto.newKey('HmacSHA256', 512)
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('HmacSHA256')
//// Crypto.hmac() 用于获取数据摘要
//def hmac = $crypto.hmac('HmacSHA256', data, key.encoded())
//$console.log(hmac)

//// HmacSHA384 加解密例子
//// Crypto.newKey() 用于新建密钥
//def key = $crypto.newKey('HmacSHA384', 512)
//// Strings.toBytes() 用于将字符串转成字节数组
//def data = $strings.toBytes('HmacSHA384')
//// Crypto.hmac() 用于获取数据摘要
//def hmac = $crypto.hmac('HmacSHA384', data, key.encoded())
//$console.log(hmac)

// HmacSHA512 加解密例子
// Crypto.newKey() 用于新建密钥
def key = $crypto.newKey('HmacSHA512', 512)
// Strings.toBytes() 用于将字符串转成字节数组
def data = $strings.toBytes('HmacSHA512')
// Crypto.hmac() 用于获取数据摘要
def hmac = $crypto.hmac('HmacSHA512', data, key.encoded())
$console.log(hmac)

```