功能:

+ 获取此part内容类型(Content-Type请求头).

定义:

+ [HttpContentType](/API/Network/HttpCommon/HttpContentType/README.md) contentType()

参数:

+ 无

返回值:

+ [HttpContentType](/API/Network/HttpCommon/HttpContentType/README.md) - 此part的内容类型,当"Content-Type"
  请求头不存在时返回null.

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpMultipartItem.contentType()](/API/Network/HttpCommon/HttpMultipartItem/README.md?id=contentType)
  获取此part内容类型.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口新建一个服务器
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    // HttpServerConfig.routing() 用于配置服务器路由信息
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.post() 用于配置Post路由
        post("/contentType") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/contentType"
            def path = request.path()
            $assert.assertTrue(path == "/contentType")
            $console.log("Path->$path")
            // HttpServerRequest.multipartBody() 可以接收multipart类型的数据, 返回值类型为 List<HttpMultipartItem>
            def multipart = request.multipartBody()
            def partItem = multipart[0]
            // HttpMultipartItem.contentType() 用于获取此part内容类型
            def contentType = partItem.contentType()
            $assert.assertTrue(contentType.contentType() == "text", "content type")
            $assert.assertTrue(contentType.contentSubtype() == "plain", "content subtype")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.textBody(path)
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.postMultipart() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.postMultipart("http://localhost:8080/contentType", {
    // delegate -> HttpClientMultipart
    // HttpClientMultipart.text() 用于添加文本类型的part
    text("textPartName", "textPartValue", ["Content-Type": "text/plain; charset=utf-8"])
})
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/contentType"
$assert.assertTrue(textResult == "/contentType", "返回结果为 /contentType")
// HttpServer.stop() 用于停止服务器.
server.stop()
```