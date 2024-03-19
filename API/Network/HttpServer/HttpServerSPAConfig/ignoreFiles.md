功能:

+ 设置需要被忽略的路径,如果应忽略路径,则通过此方法注册一个闭包返回 true。

定义:

+ [HttpServerSPAConfig](/API/Network/HttpServer/HttpServerSPAConfig/README.md) ignoreFiles(Closure
  closure)

参数:

+ Closure closure - 设置忽略文件的闭包
    + 参数
        + [ScriptFile](/API/File/ScriptFile/README.md) file - 待过滤的文件
    + delegate - 无
    + 返回值
        + boolean - true表示忽略文件,false表示不忽略

返回值:

+ [HttpServerSPAConfig](/API/Network/HttpServer/HttpServerSPAConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过
  [HttpServerSPAConfig.ignoreFiles()](/API/Network/HttpServer/HttpServerSPAConfig/README.md?id=ignoreFiles)
  设置需要被忽略的路径.

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
            // HttpServerSPAConfig.ignoreFiles() 用于设置需要被忽略的路径
            ignoreFiles {
                // it -> ScriptFile
                // 忽略robots.txt文件
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