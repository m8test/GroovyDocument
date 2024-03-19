功能:

+ WebSocket 出现错误/异常时回调

定义:

+ [WebSocketSession](/API/Network/HttpCommon/WebSocketSession/README.md) onError(Closure callback)

参数:

+ Closure callback - 回调闭包
    + 参数
        + Throwable e - 错误/异常对象
    + delegate - 无

返回值:

+ [WebSocketSession](/API/Network/HttpCommon/WebSocketSession/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个 WebSocket
  服务器,通过 [WebSocketSession.onError()](/API/Network/HttpCommon/WebSocketSession/README.md?id=onError)
  监听 WebSocket 错误信息.

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
        webSocket("/onError") {
            // delegate -> WebSocketSession
            // WebSocketSession.onOpen() 当 WebSocket 第一次成功连接时会调用此闭包
            onOpen {
                $console.log("客户端连接成功->/onError")
            }
            // WebSocketSession.onClose() 当 WebSocket 连接断开时调用
            onClose {
                $console.log("与客户端断开连接")
            }
            // WebSocketSession.onError() 当出现错误时被调用
            onError {
                $console.log("服务器端出错了:${it.message()}")
            }
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.webSocket() 用于新建一个 WebSocket 连接
client.webSocket("ws://localhost:8080/onError") {
    // delegate -> WebSocketSession
    // WebSocketSession.onOpen() 当 WebSocket 第一次成功连接时会调用此闭包
    onOpen {
        $console.log("连接服务器成功->/onError")
        // 抛异常
        throw new RuntimeException("测试onError")
    }
    // WebSocketSession.onClose() 当 WebSocket 连接断开时调用
    onClose {
        $console.log("与服务器断开连接")
    }
    // WebSocketSession.onError() 当出现错误时被调用
    onError {
        $console.log("客户端出错了:${it.getMessage()}")
        // WebSocketSession.close() 用于关闭 WebSocket 连接
        close(1000, "正常关闭")
    }
}
// 由于 HttpClient.webSocket() 为同步方法,所以此后代码不会被执行,直到 WebSocket 关闭
// HttpServer.stop() 用于停止服务器.
server.stop()
```