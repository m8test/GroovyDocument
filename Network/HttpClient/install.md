```groovy
def client = $httpClientManager.newClient {
    install($httpClientPlugin.logging())
}
```