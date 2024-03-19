功能:

+ 新建密钥.

定义:

+ [Key](/API/Crypto/Key/README.md) newKey(String algorithm, int keySize)

参数:

+ String algorithm - 需要为哪个算法生成密钥
+ int keySize - 密钥长度

返回值:

+ [Key](/API/Crypto/Key/README.md) - 新创建的密钥

示例代码:

+ 通过 [Crypto.newKey()](/API/Crypto/Crypto/README.md?id=newKey) 新建密钥.

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