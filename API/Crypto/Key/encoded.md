功能:

+ 获取密钥二进制内容.

定义:

+ byte[] encoded()

参数:

+ 无

返回值:

+ byte[] - 密钥二进制内容

示例代码:

+ 通过 [Key.encoded()](/API/Crypto/Key/README.md?id=encoded) 获取密钥二进制内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()

// DES 加解密例子
// Crypto.newKey() 用于新建密钥
def key = $crypto.newKey('DES', 56)
// Strings.toBytes() 用于将字符串转成字节数组
def data = $strings.toBytes('DES')
// Crypto.encrypt() 用于加密数据
def encryptedData = $crypto.encrypt('DES', data, key.encoded())
// Crypto.decrypt() 用于解密数据
def decryptedData = $crypto.decrypt('DES', encryptedData, key.encoded())
$assert.assertTrue($strings.fromBytes(decryptedData) == 'DES', 'DES')
```