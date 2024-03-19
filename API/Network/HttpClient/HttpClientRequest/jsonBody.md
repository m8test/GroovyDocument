功能:

+ 设置post请求体,Content-Type 为 application/json

定义:

+ [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md) jsonBody(String|Map<
  String, Object>|Collection<Object> body)

参数:

+ String|Map<String, Object>|Collection<Object> body - 可以是json字符串或者是键值对或者是集合.

返回值:

+ [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpClientRequest.jsonBody()](/API/Network/HttpClient/HttpClientRequest/README.md?id=jsonBody)
  设置请求体后再通过 [HttpClient.request()](/API/Network/HttpClient/HttpClient/README.md?id=request)
  方法发送post请求到该服务器.

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
        post("/jsonBodyString") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/jsonBodyString"
            def path = request.path()
            $assert.assertTrue(path == "/jsonBodyString")
            $console.log("Path->$path")
            // HttpServerRequest.jsonBody() 可以将json请求体内容转成 JSONObject|JSONArray
            def jsonBody = request.jsonBody()
            // 断言json请求体内容
            $assert.assertTrue(jsonBody.get("jsonBodyStringKey1") == "jsonBodyStringValue1", "jsonBodyStringKey1")
            $assert.assertTrue(jsonBody.get("jsonBodyStringKey2") == "jsonBodyStringValue2", "jsonBodyStringKey2")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.textBody(path)
        }
        // HttpServerRouting.post() 用于配置post路由
        post("/jsonBodyMap") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/jsonBodyMap"
            def path = request.path()
            $assert.assertTrue(path == "/jsonBodyMap")
            $console.log("Path->$path")
            // HttpServerRequest.jsonBody() 可以将json请求体内容转成 JSONObject|JSONArray
            def jsonBody = request.jsonBody()
            $assert.assertTrue(jsonBody.get("jsonBodyMapKey1").get("anotherMapKey") == "anotherMapValue", "jsonBodyMapKey1")
            $assert.assertTrue(jsonBody.get("jsonBodyMapKey2").get(0).get("anotherMapKeyInArray") == "anotherMapValueInArray" && jsonBody.get("jsonBodyMapKey2").get(1) == "other value", "jsonBodyMapKey2")
            $assert.assertTrue(jsonBody.get("jsonBodyMapKey3") == "jsonBodyMapValue3", "jsonBodyMapKey3")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.textBody(path)
        }
        // HttpServerRouting.post() 用于配置post路由
        post("/jsonBodyCollection") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/jsonBodyCollection"
            def path = request.path()
            $assert.assertTrue(path == "/jsonBodyCollection")
            $console.log("Path->$path")
            // HttpServerRequest.jsonBody() 可以将json请求体内容转成 JSONObject|JSONArray
            def jsonBody = request.jsonBody()
            $assert.assertTrue(jsonBody.get(0).get("jsonBodyCollectionKey1") == "jsonBodyCollectionValue1", "jsonBodyCollectionKey1")
            $assert.assertTrue(jsonBody.get(1) == "jsonBodyCollectionValue2", "jsonBodyCollection2")
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
def response = client.request("http://localhost:8080/jsonBodyString") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "post"
    // HttpClientRequest.jsonBody() 用于设置请求体内容,可以是json字符串
    jsonBody('{"jsonBodyStringKey1":"jsonBodyStringValue1","jsonBodyStringKey2":"jsonBodyStringValue2"}')
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/jsonBodyString"
$assert.assertTrue(textResult == "/jsonBodyString", "返回结果为 /jsonBodyString")
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
response = client.request("http://localhost:8080/jsonBodyMap") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "post"
    // HttpClientRequest.jsonBody() 用于设置请求体内容,可以是键值对
    jsonBody(jsonBodyMapKey1: [anotherMapKey: "anotherMapValue"], jsonBodyMapKey2: [[anotherMapKeyInArray: "anotherMapValueInArray"], "other value"], jsonBodyMapKey3: "jsonBodyMapValue3")
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/jsonBodyMap"
$assert.assertTrue(textResult == "/jsonBodyMap", "返回结果为 /jsonBodyMap")
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
response = client.request("http://localhost:8080/jsonBodyCollection") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "post"
    // HttpClientRequest.jsonBody() 用于设置请求体内容,可以是键值对
    jsonBody([[jsonBodyCollectionKey1: "jsonBodyCollectionValue1"], "jsonBodyCollectionValue2"])
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/jsonBodyCollection"
$assert.assertTrue(textResult == "/jsonBodyCollection", "返回结果为 /jsonBodyCollection")
// HttpServer.stop() 用于停止服务器.
server.stop()
```