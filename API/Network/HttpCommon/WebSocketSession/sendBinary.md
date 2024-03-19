功能:

+ 发送二进制数据

定义:

+ [WebSocketSession](/API/Network/HttpCommon/WebSocketSession/README.md) sendBinary(byte[] data)

参数:

+ byte[] data - 需要发送的二进制数据

返回值:

+ [WebSocketSession](/API/Network/HttpCommon/WebSocketSession/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个 WebSocket
  服务器,通过 [WebSocketSession.sendBinary()](/API/Network/HttpCommon/WebSocketSession/README.md?id=sendBinary)
  发送二进制数据.

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
        webSocket("/sendBinary") {
            // delegate -> WebSocketSession
            // WebSocketSession.onOpen() 当 WebSocket 第一次成功连接时会调用此闭包
            onOpen {
                $console.log("客户端连接成功->/sendBinary")
            }
            // WebSocketSession.onBinary() 当 WebSocket 客户端发送二进制消息到服务器时会调用此闭包
            onBinary {
                // Strings.fromBytes() 可以将二进制数据转成字符串
                def textFromBytes = $strings.fromBytes(it)
                $assert.assertTrue(textFromBytes == "sendBinary from client", "服务器接收到二进制数据")
                // WebSocketSession.sendBinary() 用于发送二进制消息到客户端
                sendBinary($strings.toBytes("sendBinary from server"))
            }
            // WebSocketSession.onClose() 当 WebSocket 连接断开时调用
            onClose {
                $console.log("与客户端断开连接")
            }
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.webSocket() 用于新建一个 WebSocket 连接
client.webSocket("ws://localhost:8080/sendBinary") {
    // delegate -> WebSocketSession
    // WebSocketSession.onOpen() 当 WebSocket 第一次成功连接时会调用此闭包
    onOpen {
        $assert.assertTrue(isActive(), "WebSocket已连接")
        $console.log("连接服务器成功->/sendBinary")
        // WebSocketSession.sendBinary() 用于发送二进制消息到服务器
        sendBinary($strings.toBytes("sendBinary from client"))
    }
    // WebSocketSession.onBinary() 当 WebSocket 服务器发送二进制消息到客户端时会调用此闭包
    onBinary {
        // Strings.fromBytes() 可以将二进制数据转成字符串
        def textFromBytes = $strings.fromBytes(it)
        $assert.assertTrue(textFromBytes == "sendBinary from server", "客户端接收到二进制数据")
        // WebSocketSession.close() 用于关闭 WebSocket 连接
        close(1000, "正常关闭")
    }
    // WebSocketSession.onClose() 当 WebSocket 连接断开时调用
    onClose {
        $console.log("与服务器断开连接")
        $assert.assertTrue(!isActive(), "WebSocket已关闭")
    }
}
// 由于 HttpClient.webSocket() 为同步方法,所以此后代码不会被执行,直到 WebSocket 关闭
// HttpServer.stop() 用于停止服务器.
server.stop()
```