功能:

+ 发送Http Post请求, Content-Type 默认为 application/x-www-form-urlencoded

定义:

+ [HttpClientResponse](/API/Network/HttpClient/HttpClientResponse/README.md) post(String url, Map<
  String, String> formParams = null, Closure closure = null)

参数:

+ String url - 请求的url路径
+ Map<String, String> formParams - 请求的表单参数
+ Closure closure - 对Http请求配置的闭包
    + 参数 - 无
    + delegate -
      [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md)

返回值:

+ [HttpClientResponse](/API/Network/HttpClient/HttpClientResponse/README.md) - Http响应信息封装的对象

示例代码:

+ 在8080端口开启一个服务器,通过 [HttpClient.post()](/API/Network/HttpClient/HttpClient/README.md?id=post)
  方法访问该服务器.

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
        post("/post") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/post"
            def path = request.path()
            $assert.assertTrue(path == "/post")
            $console.log("Path->$path")
            // HttpServerRequest.textBody() 可以获得查询参数字符串
            def textBody = request.textBody()
            $assert.assertTrue(textBody == "form1=value1&form2=value2", "表单字符串")
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
// HttpClient.post() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.post("http://localhost:8080/post", [form1: "value1", form2: "value2"])
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/post"
$assert.assertTrue(textResult == "/post", "返回结果为 /post")
// HttpServer.stop() 用于停止服务器.
server.stop()
```