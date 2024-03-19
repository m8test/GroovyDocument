功能:

+ 添加cookie到响应头中.

定义:

+ [HttpServerResponse](/API/Network/HttpServer/HttpServerResponse/README.md) cookie(Map<String,
  Object> cookieMap)

参数:

+ Map<String, Object> cookieMap - 设置cookie信息的map,键可选值如下:
    + name: 设置cookie名
        + 值类型: String
    + value: 设置cookie值
        + 值类型: String
    + maxAge: (选填)设置cookie Max-Age属性
        + 值类型: int
    + expires: (选填)设置cookie Expires属性
        + 值类型: [ScriptDateTime](/API/DateTime/ScriptDateTime/README.md)
    + domain: (选填)设置cookie Domain属性
        + 值类型: String
    + path: (选填)设置cookie Path属性
        + 值类型: String
    + secure: (选填)设置cookie Secure属性
        + 值类型: boolean
    + httpOnly: (选填)设置cookie HttpOnly属性
        + 值类型: boolean
    + extensions: (选填)设置cookie其他属性
        + 值类型: Map<String, String>

返回值:

+ [HttpServerResponse](/API/Network/HttpServer/HttpServerResponse/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpServerResponse.cookie()](/API/Network/HttpServer/HttpServerResponse/README.md?id=cookie)
  添加cookie到响应头中.

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
        get("/cookie") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/cookie"
            def path = request.path()
            $assert.assertTrue(path == "/cookie")
            $console.log("Path->$path")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.cookie() 用于设置cookie信息
            response.cookie(name: "cookie1", value: "cookieValue1", maxAge: 3600, expires: $dateTimes.create($dateTimes.timestamp()), domain: "localhost:8080", path: "/cookie", secure: false, httpOnly: true, extensions: [extention1: "extensionValue1", extension2: "extensionValue2"])
            response.cookie(name: "cookie2", value: "cookieValue2")
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
def response = client.request("http://localhost:8080/cookie") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.cookies() 用于获取cookie信息
def cookies = response.cookies()
// 断言cookie
$assert.assertTrue(cookies[0].name() == "cookie1" && cookies[0].value() == "cookieValue1", "cookie1")
$assert.assertTrue(cookies[1].name() == "cookie2" && cookies[1].value() == "cookieValue2", "cookie2")
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/cookie"
$assert.assertTrue(textResult == "/cookie", "返回结果为 /cookie")
// HttpServer.stop() 用于停止服务器.
server.stop()
```