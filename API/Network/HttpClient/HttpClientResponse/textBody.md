功能:

+ 读取响应体内容为文本.

定义:

+ String textBody(String charset = null)

参数:

+ String charset - 编码格式,默认为null,会根据响应头设置编码,如果响应头中没有编码信息,默认会使用 UTF-8 编码.最好不要添加此参数,如果出现乱码时再填写.

返回值:

+ String - 响应体的文本内容.

示例代码:

+ 在8080端口开启一个服务器,通过 [HttpClient.request()](/API/Network/HttpClient/HttpClient/README.md?id=request)
  方法访问该服务器后再通过 [HttpClientResponse.textBody()](/API/Network/HttpClient/HttpClientResponse/README.md?id=textBody)
  获取响应体文本内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口新建一个服务器
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    // HttpServerConfig.routing() 用于配置服务器路由信息
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.get() 用于配置Get路由
        get("/textBody") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/textBody"
            def path = request.path()
            $assert.assertTrue(path == "/textBody")
            $console.log("Path->$path")
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
def response = client.request("http://localhost:8080/textBody") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.charset() 可以获得响应体编码方式
def charset = response.charset()
// HttpCharset.name() 可获得编码名称
def charsetName = charset.name()
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody(charsetName)
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/textBody"
$assert.assertTrue(textResult == "/textBody", "返回结果为 /textBody")
// HttpServer.stop() 用于停止服务器.
server.stop()
```