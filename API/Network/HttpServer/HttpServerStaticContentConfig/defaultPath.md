功能:

+ 配置默认资源以响应

定义:

+ [HttpServerStaticContentConfig](/API/Network/HttpServer/HttpServerStaticContentConfig/README.md)
  defaultPath(String path)

参数:

+ String path - 当找不到请求的文件时,会返回此路径指定的资源

返回值:

+ [HttpServerStaticContentConfig](/API/Network/HttpServer/HttpServerStaticContentConfig/README.md) -
  返回对象本身方便链式调用

示例代码:

+ 通过
  [HttpServerStaticContentConfig.defaultPath()](/API/Network/HttpServer/HttpServerStaticContentConfig/README.md?id=defaultPath)
  配置默认资源以响应。

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口启动一个服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    routing {
        // delegate -> HttpServerRouting
        // Files.buildFile() 用于构建一个 ScriptFile 对象
        def scriptFile = $files.buildFile {
            // delegate -> FileBuilder
            // FileBuilder.res() 用于配置文件路径为项目资源文件路径
            res("react-app")
        }
        // HttpServerRouting.staticFiles() 用于设置路由以提供静态文件
        staticFiles("/", scriptFile, "index.html") {
            // delegate -> HttpServerStaticContentConfig
            // HttpServerStaticContentConfig.defaultPath() 用于配置默认资源以响应
            defaultPath("index.html")
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