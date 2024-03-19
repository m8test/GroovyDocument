功能:

+ 创建 [TesseractOcr](/API/Ocr/TesseractOcr/README.md) 对象.

定义:

+ [TesseractOcr](/API/Ocr/TesseractOcr/README.md) tesseract(Closure closure)

参数:

+ Closure closure - 配置 [TesseractOcr](/API/Ocr/TesseractOcr/README.md) 的闭包
    + 参数 - 无
    + delegate - [TesseractOcrConfig](/API/Ocr/TesseractOcrConfig/README.md)

返回值:

+ [TesseractOcr](/API/Ocr/TesseractOcr/README.md) - 根据配置创建的 [TesseractOcr](/API/Ocr/TesseractOcr/README.md) 对象

示例代码:

+ 通过 [Ocrs.tesseract()](/API/Ocr/Ocrs/README.md?id=tesseract) 创建 [TesseractOcr](/API/Ocr/TesseractOcr/README.md) 对象.

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