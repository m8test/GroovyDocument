功能:

+ 新建 WebSocket 连接,此方法为同步方法,会阻塞当前线程直到 WebSocket
  连接关闭,如果需要异步,则可以通过 [Threads.startThread()](/API/Thread/Threads/README.md?id=startThread)
  方法启动新线程再调用此方法.

定义:

+ [HttpClient](/API/Network/HttpClient/HttpClient/README.md) webSocket(String url, Closure
  requestConfig = null, Closure webSocketConfig = null)

参数:

+ String url - WebSocket 服务器URL地址
+ Closure requestConfig - 配置请求的闭包
    + 参数 - 无
    + delegate - [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md)
+ Closure webSocketConfig - WebSocket 配置闭包
    + 参数 - 无
    + delegate - [WebSocketSession](/API/Network/HttpCommon/WebSocketSession/README.md)

返回值:

+ [HttpClient](/API/NetWork/HttpClient/HttpClient/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个 WebSocket 服务器,通过 HttpClient.webSocket() 访问该服务器.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口新建一个服务器
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    // HttpServerConfig.routing() 用于配置服务器路由信息
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.webSocket() 用于配置 WebSocket 服务器.
        webSocket("/webSocket/path/segments") {
            // delegate -> WebSocketSession
            // WebSocketSession.onOpen() 当 WebSocket 第一次成功连接时会调用此闭包
            onOpen {
                $console.log("客户端连接成功->/webSocket/path/segments")
            }
            // WebSocketSession.onText() 当 WebSocket 接收到文本消息时会回调此闭包
            onText {
                $console.log("接收到客户端文本消息:$it")
                // WebSocketSession.sendText() 用于发送文本消息
                sendText("来自服务器的文本消息")
            }
            // WebSocketSession.onClose() 当 WebSocket 连接断开时调用
            onClose {
                $console.log("与客户端断开连接")
            }
            // WebSocketSession.onError() 当出现错误时被调用
            onError {
                $console.log("服务器端出错了:${it.getMessage()}")
            }
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.webSocket() 用于新建一个 WebSocket 连接
client.webSocket("ws://localhost:8080/webSocket", {
    // delegate -> HttpClientRequest
    // HttpClientRequest.pathSegment() 用于添加路径到url中
    pathSegments("path", "segments")
}) {
    // delegate -> WebSocketSession
    // WebSocketSession.onOpen() 当 WebSocket 第一次成功连接时会调用此闭包
    onOpen {
        $console.log("连接服务器成功->/webSocket/path/segments")
        // WebSocketSession.sendText() 用于发送文本消息
        sendText("来自客户端的文本消息")
    }
    // WebSocketSession.onText() 当 WebSocket 接收到文本消息时会回调此闭包
    onText {
        $console.log("接收到服务器文本消息:$it")
        // WebSocketSession.close() 用于关闭 WebSocket 连接
        close(1000, "正常关闭")
    }
    // WebSocketSession.onClose() 当 WebSocket 连接断开时调用
    onClose {
        $console.log("与服务器断开连接")
    }
    // WebSocketSession.onError() 当出现错误时被调用
    onError {
        $console.log("客户端出错了:${it.getMessage()}")
    }
}
// 由于 HttpClient.webSocket() 为同步方法,所以此后代码不会被执行,直到 WebSocket 关闭
// HttpServer.stop() 用于停止服务器.
server.stop()
```