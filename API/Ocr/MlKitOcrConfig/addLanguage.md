功能:

+ 添加语言.

定义:

+ [MlKitOcrConfig](/API/Ocr/MlKitOcrConfig/README.md) addLanguage(String lang, String alias)

参数:

+ String lang - 需要添加的语言,可选值有
    + chinese - 中文
    + latin - 拉丁文
+ String alias -
  语言的别名,可以为null,如果设置了别名, [Ocr.getText()](/API/Ocr/Ocr/README.md?id=getText) 就可以通过别名识别

返回值:

+ [MlKitOcrConfig](/API/Ocr/MlKitOcrConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [MlKitOcrConfig.addLanguage()](/API/Ocr/MlKitOcrConfig/README.md?id=addLanguage) 添加语言.

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