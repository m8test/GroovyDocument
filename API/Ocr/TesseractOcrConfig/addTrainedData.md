功能:

+ 添加语言训练数据.

定义:

+ [TesseractOcrConfig](/API/Ocr/TesseractOcrConfig/README.md) addTrainedData(String
  lang, [ScriptFile](/API/File/ScriptFile/README.md) trainedDataPath)

参数:

+ String lang - 需要添加的语言
+ [ScriptFile](/API/File/ScriptFile/README.md) trainedDataPath - 语言训练数据路径

返回值:

+ [TesseractOcrConfig](/API/Ocr/TesseractOcrConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过
  [TesseractOcrConfig.addTrainedData()](/API/Ocr/TesseractOcrConfig/README.md?id=addTrainedData)
  添加语言训练数据.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Ocrs.tesseract() 用于创建 TesseractOcr 对象
def ocr = $ocrs.tesseract {
    // delegate -> TesseractOcrConfig
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.res() 用于配置文件路径为项目资源文件路径
        res("chi_sim.traineddata")
    }
    // TesseractOcrConfig.addTrainedData() 用于添加语言训练数据
    addTrainedData("chi_sim", scriptFile)
}
// Ocr.getText() 用于获取图片中的文字
def result = ocr.getText($images.read {
    url('https://s1.ax1x.com/2022/10/29/x55lh4.png')
}, 'chi_sim')
// 断言识别结果
$assert.assertTrue(result == '七 言 诗', 'Ocr识别结果')
```