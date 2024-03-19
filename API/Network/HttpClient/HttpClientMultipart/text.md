功能:

+ 添加文本类型的part.

定义:

+ [HttpClientMultipart](/API/Network/HttpClient/HttpClientMultipart/README.md) text(String name,
  String value, Map<String, String> headers = null)

参数:

+ String name - part名
+ String value - part值
+ Map<String, String> headers - (选填)part的header信息

返回值:

+ [HttpClientMultipart](/API/Network/HttpClient/HttpClientMultipart/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpClientMultipart.text()](/API/Network/HttpClient/HttpClientMultipart/README.md?id=text)
  添加文本类型的 part
  后再通过 [HttpClient.postMultipart()](/API/Network/HttpClient/HttpClient/README.md?id=postMultipart)
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
    post("/text") {
      // delegate -> HttpServerCall
      // HttpServerCall.request() 可以获得请求对象HttpServerRequest
      def request = request()
      // HttpServerRequest.path() 可获得访问路径,此处为 "/text"
      def path = request.path()
      $assert.assertTrue(path == "/text")
      $console.log("Path->$path")
      // HttpServerRequest.multipartBody() 可以接收multipart类型的数据, 返回值类型为 List<HttpMultipartItem>
      def multipart = request.multipartBody()
      def p1 = multipart[0]
      $console.log("文本类型:${p1.name()}")
      // 文本类型的数据
      // HttpMultipartItem.name() 可以获取数据名,也就是 Content-Disposition 请求头的 name 属性
      $assert.assertTrue(p1.name() == "textPartName1", "文本数据name的值1")
      // HttpMultipartItem.value() 可以获取 name 对应的值
      $assert.assertTrue(p1.value() == "textPartValue1", "文本数据name对应的值1")
      def p2 = multipart[1]
      $console.log("文本类型:${p2.name()}")
      // 文本类型的数据
      // HttpMultipartItem.name() 可以获取数据名,也就是 Content-Disposition 请求头的 name 属性
      $assert.assertTrue(p2.name() == "textPartName2", "文本数据name的值2")
      // HttpMultipartItem.value() 可以获取 name 对应的值
      $assert.assertTrue(p2.value() == "textPartValue2", "文本数据name对应的值2")
      // HttpMultipartItem.headers() 可以获得 part 的 header 信息
      def headers = p2.headers()
      // 断言 headers
      $assert.assertTrue(headers.get("header1") == "value1", "header1")
      $assert.assertTrue(headers.get("header2") == "value2", "header2")
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
def response = client.postMultipart("http://localhost:8080/text", {
  // delegate -> HttpClientMultipart
  // HttpClientMultipart.text() 用于添加文本类型的part
  text("textPartName1", "textPartValue1")
  text("textPartName2", "textPartValue2", [header1: "value1", header2: "value2"])
})
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/text"
$assert.assertTrue(textResult == "/text", "返回结果为 /text")
// HttpServer.stop() 用于停止服务器.
server.stop()
```