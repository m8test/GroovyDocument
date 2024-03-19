功能:

+ 获取请求体内容编码.

定义:

+ [HttpCharset](/API/Network/HttpCommon/HttpCharset/README.md) charset()

参数:

+ 无

返回值:

+ [HttpCharset](/API/Network/HttpCommon/HttpCharset/README.md) - 封装了请求体内容编码的对象.

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpServerRequest.charset()](/API/Network/HttpServer/HttpServerRequest/README.md?id=charset)
  获取请求体内容编码.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口新建一个服务器
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    // HttpServerConfig.routing() 用于配置服务器路由信息
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.post() 用于配置post路由
        post("/charset") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/charset"
            def path = request.path()
            $assert.assertTrue(path == "/charset")
            $console.log("Path->$path")
            // HttpServerRequest.charset() 可以获取请求体内容类型
            def charset = request.charset()
            // 断言内容编码
            $assert.assertTrue(charset.name() == "UTF-8", "请求体内容编码")
            // HttpServerRequest.textBody() 可以将请求体内容转成字符串
            def textBody = request.textBody()
            $assert.assertTrue(textBody == "body text", "请求体文本内容")
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
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.request("http://localhost:8080/charset") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "post"
    // HttpClientRequest.body() 用于设置请求体内容
    body("body text")
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/charset"
$assert.assertTrue(textResult == "/charset", "返回结果为 /charset")
// HttpServer.stop() 用于停止服务器.
server.stop()
```