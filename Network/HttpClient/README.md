## 概况

Http客户端提供了访问网络的功能.

## 新建客户端

新建一个带有默认配置的客户端.

[filename](newClient.md ':include')

## 配置客户端

### 基本配置

要配置客户端,您可以将附加功能参数传递到闭包中, [HttpClientConfig](/API/Network/HttpClient/HttpClientConfig/README.md)
类是用于配置客户端的类.例如,您可以使用 [HttpClientConfig.expectSuccess()](/API/Network/HttpClient/HttpClientConfig/README.md?id=expectSuccess)
启用响应验证.

[filename](baseConfig.md ':include')

### 引擎配置

您可以使用 [HttpClientConfig.engine()](/API/Network/HttpClient/HttpClientConfig/README.md?id=engine) 配置引擎

[filename](engineConfig.md ':include')

## 插件

要安装插件,您需要通过 [HttpClientConfig.install()](/API/Network/HttpClient/HttpClientConfig/README.md?id=install)
方法实现,所有可用插件可在 [HttpClientPlugin](/API/Network/HttpClient/HttpClientPlugin/README.md)
查看.例如您可以通过 [HttpClientPlugin.logging()](/API/Network/HttpClient/HttpClientPlugin/README.md?id=logging)
插件来记录Http调用.

[filename](install.md ':include')

您还可以在 [HttpClientConfig.install()](/API/Network/HttpClient/HttpClientConfig/README.md?id=install)
闭包内配置插件,您可以指定记录器和日志记录级别

[filename](installConfig.md ':include')