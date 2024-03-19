功能:

+ 向 [Storage](/API/Storages/Storage/README.md) 本地存储对象中添加键值对.

定义:

+ boolean put(String key, String value)

参数:

+ String key - 需要添加到 [Storage](/API/Storages/Storage/README.md) 本地存储对象中的键
+ String value - 需要添加到 [Storage](/API/Storages/Storage/README.md) 本地存储对象中的键对应的值

返回值:

+ boolean - 成功将键值对添加到 [Storage](/API/Storages/Storage/README.md) 本地存储对象中返回true,否则返回false

示例代码:

+ 通过 [Storages.get()](/API/Storages/Storages/README.md?id=get)
  获取本地存储对象 [Storage](/API/Storages/Storage/README.md)
  ,并通过 [Storage.put()](/API/Storages/Storage/README.md?id=put) 向其添加内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()

// Storages.get() 用于获取本地存储对象 Storage
def storage = $storages.get('name')
// Storage.put() 用于向本地存储对象添加数据
$assert.assertTrue(storage.put('key1', 'value1'))
$assert.assertTrue(storage.put('key2', 'value2'))
// Storage.get() 用于根据key值获取本地存储对象中对应的值
$assert.assertTrue(storage.get('key1', null) == 'value1', '断言key1的值为value1')
$assert.assertTrue(storage.get('key2', null) == 'value2', '断言key2的值为value2')
```
