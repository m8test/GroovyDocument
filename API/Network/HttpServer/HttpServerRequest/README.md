## 概况

[HttpServerRequest](/API/Network/HttpServer/HttpServerRequest/README.md) 封装了Http请求信息,主要有以下分类:

+ 请求体相关
    + [HttpServerRequest.bytesBody()](/API/Network/HttpServer/HttpServerRequest/README.md?id=bytesBody) :
      将请求体内容读取为字节数组.
    + [HttpServerRequest.jsonBody()](/API/Network/HttpServer/HttpServerRequest/README.md?id=jsonBody) :
      将请求体内容按照json格式读取.
    + [HttpServerRequest.multipartBody](/API/Network/HttpServer/HttpServerRequest/README.md?id=multipartBody) :
      将请求体内容按照 multipart 类型读取
    + [HttpServerRequest.textBody](/API/Network/HttpServer/HttpServerRequest/README.md?id=textBody) :
      将请求体内容读取为文本.
    + [HttpServerRequest.urlencodedBody](/API/Network/HttpServer/HttpServerRequest/README.md?id=urlencodedBody) :
      将请求体内容按照 urlencoded 类型读取
+ 请求头相关
    + [HttpServerRequest.charset()](/API/Network/HttpServer/HttpServerRequest/README.md?id=charset) :
      获取请求体内容编码.
    + [HttpServerRequest.contentLength()](/API/Network/HttpServer/HttpServerRequest/README.md?id=contentLength) :
      获取请求体内容长度.
    + [HttpServerRequest.contentType()](/API/Network/HttpServer/HttpServerRequest/README.md?id=contentType) :
      获取请求体内容类型.
    + [HttpServerRequest.cookies()](/API/Network/HttpServer/HttpServerRequest/README.md?id=cookies) :
      获取请求中的cookies.
    + [HttpServerRequest.headers()](/API/Network/HttpServer/HttpServerRequest/README.md?id=headers) :
      获取请求中的headers. 获取请求中的headers.
    + [HttpServerRequest.isMultipart()](/API/Network/HttpServer/HttpServerRequest/README.md?id=isMultipart) :
      判断请求体是否为 Multipart 类型
    + [HttpServerRequest.userAgent()](/API/Network/HttpServer/HttpServerRequest/README.md?id=userAgent) :
      获取 User-Agent 请求头的值
+ 请求URL相关
    + [HttpServerRequest.host()](/API/Network/HttpServer/HttpServerRequest/README.md?id=host) :
      获取Http请求所访问的主机
    + [HttpServerRequest.path()](/API/Network/HttpServer/HttpServerRequest/README.md?id=path) :
      获取请求路径
    + [HttpServerRequest.pathParamters()](/API/Network/HttpServer/HttpServerRequest/README.md?id=pathParameters) :
      获取请求路径参数
    + [HttpServerRequest.port()](/API/Network/HttpServer/HttpServerRequest/README.md?id=port) :
      获取Http请求所访问的端口号
    + [HttpServerRequest.queryParameters()](/API/Network/HttpServer/HttpServerRequest/README.md?id=queryParameters) :
      获取查询参数
    + [HttpServerRequest.queryString()](/API/Network/HttpServer/HttpServerRequest/README.md?id=queryString) :
      获取查询字符串
    + [HttpServerRequest.uri()](/API/Network/HttpServer/HttpServerRequest/README.md?id=uri) :
      获取请求uri
+ 请求行相关
    + [HttpServerRequest.httpMethod()](/API/Network/HttpServer/HttpServerRequest/README.md?id=httpMethod) :
      获取Http请求方法
    + [HttpServerRequest.httpVersion()](/API/Network/HttpServer/HttpServerRequest/README.md?id=httpVersion) :
      获取Http版本

## bytesBody()

[filename](bytesBody.md ':include')

## charset()

[filename](charset.md ':include')

## contentLength()

[filename](contentLength.md ':include')

## contentType()

[filename](contentType.md ':include')

## cookies()

[filename](cookies.md ':include')

## headers()

[filename](headers.md ':include')

## host()

[filename](host.md ':include')

## httpMethod()

[filename](httpMethod.md ':include')

## httpVersion()

[filename](httpVersion.md ':include')

## isMultipart()

[filename](isMultipart.md ':include')

## jsonBody()

[filename](jsonBody.md ':include')

## multipartBody()

[filename](multipartBody.md ':include')

## path()

[filename](path.md ':include')

## pathParameters()

[filename](pathParameters.md ':include')

## port()

[filename](port.md ':include')

## queryParameters()

[filename](queryParameters.md ':include')

## queryString()

[filename](queryString.md ':include')

## textBody()

[filename](textBody.md ':include')

## uri()

[filename](uri.md ':include')

## urlencodedBody()

[filename](urlencodedBody.md ':include')

## userAgent()

[filename](userAgent.md ':include')
