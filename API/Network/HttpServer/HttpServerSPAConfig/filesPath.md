功能:

+ 设置静态内容所在的路径

定义:

+ [HttpServerSPAConfig](/API/Network/HttpServer/HttpServerSPAConfig/README.md)
  filesPath([ScriptFile](/API/File/ScriptFile/README.md) path)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) path - 静态内容所在路径

返回值:

+ [HttpServerSPAConfig](/API/Network/HttpServer/HttpServerSPAConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过
  [HttpServerSPAConfig.filesPath()](/API/Network/HttpServer/HttpServerSPAConfig/README.md?id=filesPath)
  设置静态内容所在的路径.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口启动一个服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.singlePageApplication() 用于配置SPA单页应用,支持vue,angular,react,ember等框架
        singlePageApplication {
            // delegate -> HttpServerSPAConfig
            // Files.buildFile() 用于构建一个 ScriptFile 对象
            def scriptFile = $files.buildFile {
                // delegate -> FileBuilder
                // FileBuilder.res() 用于配置文件路径为项目资源文件路径
                res("react-app")
            }
            // HttpServerSPAConfig.filesPath() 用于设置静态内容所在的路径
            filesPath(scriptFile)
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.get() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.get("http://localhost:8080/")
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.res() 用于配置文件路径为项目资源文件路径
    res("react-app/index.html")
}
// 断言首页内容和"index.html"中的内容一样
$assert.assertTrue(textResult == scriptFile.readText(), "首页内容")
// HttpServer.stop() 用于停止服务器.
server.stop()
```