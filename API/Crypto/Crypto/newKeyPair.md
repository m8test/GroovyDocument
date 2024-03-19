功能:

+ 新建密钥对.

定义:

+ [KeyPair](/API/Crypto/KeyPair/README.md) newKeyPair(String algorithm, int keySize)

参数:

+ String algorithm - 需要为哪个算法生成密钥对
+ int keySize - 密钥长度

返回值:

+ [KeyPair](/API/Crypto/KeyPair/README.md) - 新创建的密钥对

示例代码:

+ 通过 [Crypto.newKeyPair()](/API/Crypto/Crypto/README.md?id=newKeyPair) 新建密钥对.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()

// RSA 加解密例子
// Strings.toBytes() 用于将字符串转成字节数组
def data = $strings.toBytes('RSA')
// Crypto.newKeyPair() 用于生成密钥对
def keyPair = $crypto.newKeyPair('RSA', 2048)
// KeyPair.publicKey() 用于获取公钥
def publicKey = keyPair.publicKey()
// Crypto.encrypt() 用于加密数据
def encryptedData = $crypto.encrypt('RSA', data, publicKey.encoded())
// KeyPair.privateKey() 用于获取私钥
def privateKey = keyPair.privateKey()
// Crypto.decrypt() 用于解密数据
def decryptedData = $crypto.decrypt('RSA', encryptedData, privateKey.encoded())
$assert.assertTrue($strings.fromBytes(decryptedData) == 'RSA', 'RSA')
```