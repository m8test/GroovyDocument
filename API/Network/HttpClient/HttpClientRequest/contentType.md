功能:

+ 设置post请求体类型,一般不需要指定,由系统根据请求体内容自动确定,如果手动指定类型错误则会报错.

定义:

+ [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md) contentType(String
  contentType)

参数:

+ String contentType - 请求体内容类型,例如 application/json 等.

返回值:

+ [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,通过 [HttpClient.request()](/API/Network/HttpClient/HttpClient/README.md?id=request)
  方法发送请求体类型为json字符串(application/json)的post请求到该服务器.

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
    post("/contentType") {
      // delegate -> HttpServerCall
      // HttpServerCall.request() 可以获得请求对象HttpServerRequest
      def request = request()
      // HttpServerRequest.path() 可获得访问路径,此处为 "/contentType"
      def path = request.path()
      $assert.assertTrue(path == "/contentType")
      $console.log("Path->$path")
      // HttpServerRequest.jsonBody() 可以将请求体内容转成 JSONObject
      def jsonBody = request.jsonBody()
      // 断言json参数
      $assert.assertTrue(jsonBody.get("jsonKey") == "jsonValue", "请求体application/json内容")
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
def response = client.request("http://localhost:8080/contentType") {
  // delegate -> HttpClientRequest
  // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
  method "post"
  // HttpClientRequest.contentType() 用于配置请求体内容类型
  contentType("application/json")
  // HttpClientRequest.body() 用于设置请求体内容
  body('{"jsonKey":"jsonValue"}')
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/contentType"
$assert.assertTrue(textResult == "/contentType", "返回结果为 /contentType")
// HttpServer.stop() 用于停止服务器.
server.stop()
```