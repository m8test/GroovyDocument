功能:

+ 创建 [MlKitOcr](/API/Ocr/MlKitOcr/README.md) 对象.

定义:

+ [MlKitOcr](/API/Ocr/MlKitOcr/README.md) mlKit(Closure closure)

参数:

+ Closure closure - 配置 [MlKitOcr](/API/Ocr/MlKitOcr/README.md) 的闭包
    + 参数 - 无
    + delegate - [MlKitOcrConfig](/API/Ocr/MlKitOcrConfig/README.md)

返回值:

+ [MlKitOcr](/API/Ocr/MlKitOcr/README.md) - 根据配置创建的 [MlKitOcr](/API/Ocr/MlKitOcr/README.md)
  对象

示例代码:

+ 通过 [Ocrs.mlKit()](/API/Ocr/Ocrs/README.md?id=mlKit) 创建 [MlKitOcr](/API/Ocr/MlKitOcr/README.md)
  对象.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Ocrs.mlKit() 用于创建 MlKitOcr 对象
def ocr = $ocrs.mlKit {
    // delegate -> MlKitOcrConfig
    // MlKitOcrConfig.addLanguage() 用于添加语言
    addLanguage("chinese", "cn")
}
// Ocr.getText() 用于获取图片中的文字,此处使用别名,当然也可以使用原名"chinese"
def result = ocr.getText($images.read {
    url('https://s1.ax1x.com/2022/10/29/x55lh4.png')
}, 'cn')
// 断言识别结果
$assert.assertTrue(result == 't言诗', 'Ocr识别结果')
```