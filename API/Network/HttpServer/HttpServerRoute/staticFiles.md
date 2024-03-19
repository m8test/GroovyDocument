功能:

+ 设置路由以提供静态文件

定义:

+ [HttpServerRoute](/API/Network/HttpServer/HttpServerRoute/README.md) staticFiles(String
  remotePath, [ScriptFile](/API/File/ScriptFile/README.md) rootFolder, String index, Closure
  closure)

参数:

+ String remotePath - 通过网络请求的路径
+ [ScriptFile](/API/File/ScriptFile/README.md) rootFolder -
  静态文件对应的本地文件夹,其中所有文件都可以在“remotePath/path/to/file”中递归访问
+ String index - 索引,如果请求的文件是目录且索引不为空，则响应将是请求目录中的索引文件。如果请求的文件不存在，或者它是一个目录并且没有指定索引，响应将是
  404 Not Found。
+ Closure closure - 配置单页应用的闭包
    + 参数 - 无
    + delegate -
      [HttpServerStaticContentConfig](/API/Network/HttpServer/HttpServerStaticContentConfig/README.md)

返回值:

+ [HttpServerRoute](/API/Network/HttpServer/HttpServerRoute/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过
  [HttpServerRoute.staticFiles()](/API/Network/HttpServer/HttpServerRoute/README.md?id=staticFiles)
  设置路由以提供静态文件

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