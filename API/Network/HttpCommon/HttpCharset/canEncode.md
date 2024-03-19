功能:

+ 判断此字符集是否支持编码。

定义:

+ boolean canEncode()

参数:

+ 无

返回值:

+ boolean - 此字符集是否支持编码返回true,否则返回false

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpCharset.canEncode()](/API/Network/HttpCommon/HttpCharset/README.md?id=canEncode)
  判断字符集是否支持编码.

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
        get("/canEncode") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/canEncode"
            def path = request.path()
            $assert.assertTrue(path == "/canEncode")
            $console.log("Path->$path")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.textBody(path, "text/plain; charset=gbk")
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.request("http://localhost:8080/canEncode") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.charset() 可以获得响应体编码方式
def charset = response.charset()
// HttpCharset.canEncode() 用于判断此字符集是否支持编码。 
def canEncode = charset.canEncode()
// 断言此字符集支持编码
$assert.assertTrue(canEncode, "字符集是否支持编码")
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/canEncode"
$assert.assertTrue(textResult == "/canEncode", "返回结果为 /canEncode")
// HttpServer.stop() 用于停止服务器.
server.stop()
```