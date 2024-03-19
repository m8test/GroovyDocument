功能:

+ 删除一个 [HttpClient](/API/Network/HttpClient/HttpClient/README.md)
  ,一般情况下不会用到方法,脚本停止后会自动删除所有由 [HttpClientManager.newClient()](/API/Network/HttpClient/HttpClientManager/README.md?id=newClient)
  创建的所有 [HttpClient](/API/Network/HttpClient/HttpClient/README.md) .

定义:

+ boolean deleteClient([HttpClient](/API/Network/HttpClient/HttpClient/README.md) httpClient)

参数:

+ [HttpClient](/API/Network/HttpClient/HttpClient/README.md) httpClient -
  需要被删除的 [HttpClient](/API/Network/HttpClient/HttpClient/README.md)

返回值:

+ boolean - 删除成功返回 true ,失败返回 false

示例代码:

+ 新建一个 [HttpClient](/API/Network/HttpClient/HttpClient/README.md) 并访问本地服务器,
  访问结束后删除该 [HttpClient](/API/Network/HttpClient/HttpClient/README.md).

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
    get("/deleteClient") {
      // delegate -> HttpServerCall
      // HttpServerCall.request() 可以获得请求对象HttpServerRequest
      def request = request()
      // HttpServerRequest.path() 可获得访问路径,此处为 "/deleteClient"
      def path = request.path()
      $assert.assertTrue(path == "/deleteClient")
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
// HttpClient.get() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.get("http://localhost:8080/deleteClient")
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/deleteClient"
$assert.assertTrue(textResult == "/deleteClient", "返回结果为 /deleteClient")
// HttpClientManager.deleteClient() 可以删除一个 HttpClient
def deleteClientResult = $httpClientManager.deleteClient(client)
// 断言删除成功
$assert.assertTrue(deleteClientResult, "删除 HttpClient 失败")
// HttpServer.stop() 用于停止服务器.
server.stop()
```