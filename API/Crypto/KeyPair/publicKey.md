功能:

+ 获取公钥.

定义:

+ [Key](/API/Crypto/Key/README.md) publicKey()

参数:

+ 无

返回值:

+ [Key](/API/Crypto/Key/README.md) - 公钥

示例代码:

+ 通过 [KeyPair.publicKey()](/API/Crypto/KeyPair/README.md?id=publicKey) 获取公钥.

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