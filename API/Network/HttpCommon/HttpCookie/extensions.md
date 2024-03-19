功能:

+ 获取cookie其他属性.

定义:

+ Map<String, String> extensions()

参数:

+ 无

返回值:

+ Map<String, String> - cookie其他属性以及对应的值.

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpCookie.extensions()](/API/Network/HttpCommon/HttpCookie/README.md?id=extensions)
  获取cookie其他属性.

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
        get("/extensions") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/extensions"
            def path = request.path()
            $assert.assertTrue(path == "/extensions")
            $console.log("Path->$path")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.cookie() 用于设置cookie信息
            response.cookie(name: "cookie", value: "cookieValue", extensions: [extension1: "value1", extension2: "value2"])
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
def response = client.request("http://localhost:8080/extensions") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.cookies() 用于获取cookie信息
def cookies = response.cookies()
def cookie = cookies[0]
// HttpCookie.extensions() 用于获取Cookie其他属性
def extensions = cookie.extensions()
$assert.assertTrue(extensions["extension1"] == "value1", "extension1")
$assert.assertTrue(extensions["extension2"] == "value2", "extension2")
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/extensions"
$assert.assertTrue(textResult == "/extensions", "返回结果为 /extensions")
// HttpServer.stop() 用于停止服务器.
server.stop()
```