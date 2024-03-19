## 概况

[HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md) 用于构建Http请求,主要有以下分类:

+ 请求体相关
    + [HttpClientRequest.body()](/API/Network/HttpClient/HttpClientRequest/README.md?id=body) :
      设置任意数据类型请求体.
    + [HttpClientRequest.contentType()](/API/Network/HttpClient/HttpClientRequest/README.md?id=contentType) :
      设置post请求体类型,一般不需要指定,由系统根据请求体内容自动确定,如果手动指定类型错误则会报错.
    + [HttpClientRequest.jsonBody()](/API/Network/HttpClient/HttpClientRequest/README.md?id=jsonBody) :
      设置post请求体,Content-Type 为 application/json
    + [HttpClientRequest.multipartBody()](/API/Network/HttpClient/HttpClientRequest/README.md?id=multipartBody) :
      设置post请求体,Content-Type 为 multipart/form-data
    + [HttpClientRequest.urlencodedBody()](/API/Network/HttpClient/HttpClientRequest/README.md?id=urlencodedBody) :
      设置post请求体,Content-Type 为 application/x-www-form-urlencoded
+ 超时相关
    + [HttpClientRequest.connectTimeout()](/API/Network/HttpClient/HttpClientRequest/README.md?id=connectTimeout) :
      指定与服务器建立连接的超时时间。
    + [HttpClientRequest.requestTimeout()](/API/Network/HttpClient/HttpClientRequest/README.md?id=requestTimeout) :
      指定整个 HTTP 调用的超时时间，从发送请求到接收响应。
    + [HttpClientRequest.socketTimeout()](/API/Network/HttpClient/HttpClientRequest/README.md?id=socketTimeout) :
      指定与服务器交换数据时两个数据包之间的最长时间超时。
+ 请求头相关
    + [HttpClientRequest.cookie()](/API/Network/HttpClient/HttpClientRequest/README.md?id=cookie) :
      添加cookie信息。
    + [HttpClientRequest.cookies()](/API/Network/HttpClient/HttpClientRequest/README.md?id=cookies) :
      添加cookie信息。
    + [HttpClientRequest.header()](/API/Network/HttpClient/HttpClientRequest/README.md?id=header) :
      添加header信息。
    + [HttpClientRequest.headers()](/API/Network/HttpClient/HttpClientRequest/README.md?id=headers) :
      添加header信息。
    + [HttpClientRequest.userAgent()](/API/Network/HttpClient/HttpClientRequest/README.md?id=userAgent) :
      设置 User-Agent 请求头.
+ URL相关
    + [HttpClientRequest.fragment()](/API/Network/HttpClient/HttpClientRequest/README.md?id=fragment) :
      设置url锚点(fragment)
    + [HttpClientRequest.pathSegments()](/API/Network/HttpClient/HttpClientRequest/README.md?id=pathSegments) :
      添加路径到url中.
    + [HttpClientRequest.queryParameter()](/API/Network/HttpClient/HttpClientRequest/README.md?id=queryParameter) :
      添加查询参数到url中.
    + [HttpClientRequest.queryParameters()](/API/Network/HttpClient/HttpClientRequest/README.md?id=queryParameters) :
      添加查询参数到url中.
+ 请求方法相关
    + [HttpClientRequest.method()](/API/Network/HttpClient/HttpClientRequest/README.md?id=method) :
      设置Http请求方法
+ 进度监听相关
    + [HttpClientRequest.onDownload()](/API/Network/HttpClient/HttpClientRequest/README.md?id=onDownload) :
      监听数据下载进度
    + [HttpClientRequest.onUpload()](/API/Network/HttpClient/HttpClientRequest/README.md?id=onUpload) :
      监听数据上传进度

## body()

[filename](body.md ':include')

## connectTimeout()

[filename](connectTimeout.md ':include')

## contentType()

[filename](contentType.md ':include')

## cookie()

[filename](cookie.md ':include')

## cookies()

[filename](cookies.md ':include')

## fragment()

[filename](fragment.md ':include')

## header()

[filename](header.md ':include')

## headers()

[filename](headers.md ':include')

## jsonBody()

[filename](jsonBody.md ':include')

## method()

[filename](method.md ':include')

## multipartBody()

[filename](multipartBody.md ':include')

## onDownload()

[filename](onDownload.md ':include')

## onUpload()

[filename](onUpload.md ':include')

## pathSegments()

[filename](pathSegments.md ':include')

## queryParameter()

[filename](queryParameter.md ':include')

## queryParameters()

[filename](queryParameters.md ':include')

## requestTimeout()

[filename](requestTimeout.md ':include')

## socketTimeout()

[filename](socketTimeout.md ':include')

## urlencodedBody()

[filename](urlencodedBody.md ':include')

## userAgent()

[filename](userAgent.md ':include')