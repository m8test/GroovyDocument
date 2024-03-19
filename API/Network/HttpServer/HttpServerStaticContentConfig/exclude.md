功能:

+ 配置不应提供的资源

定义:

+ [HttpServerStaticContentConfig](/API/Network/HttpServer/HttpServerStaticContentConfig/README.md)
  exclude(Closure closure)

参数:

+ Closure closure - 配置不提供的资源的闭包
    + 参数
        + [ScriptFile](/API/File/ScriptFile/README.md) file - 访问的文件
    + delegate - 无
    + 返回值
        + boolean - true表示不提供该资源,false表示提供该资源

返回值:

+ [HttpServerStaticContentConfig](/API/Network/HttpServer/HttpServerStaticContentConfig/README.md) -
  返回对象本身方便链式调用

示例代码:

+ 通过
  [HttpServerStaticContentConfig.exclude()](/API/Network/HttpServer/HttpServerStaticContentConfig/README.md?id=exclude)
  配置不应提供的资源。

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
            // HttpServerStaticContentConfig.exclude() 用于配置不应提供的资源
            exclude {
                // it -> ScriptFile
                it.name() == "robots.txt"
            }
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.get() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.get("http://localhost:8080/robots.txt")
// 不提供服务的资源返回403
$assert.assertTrue(response.statusCode().value() == 403)
// HttpServer.stop() 用于停止服务器.
server.stop()
```