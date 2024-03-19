功能:

+ 根据键获取 [Storage](/API/Storages/Storage/README.md) 本地存储对象中对应的值.

定义:

+ String get(String key, String defaultValue = null)

参数:

+ String key - 需要获取内容的键
+ String defaultValue - 如果本地存储对象中没有该键对应的值时返回的内容,默认为null

返回值:

+ String - 本地存储对象 [Storage](/API/Storages/Storage/README.md) 中键对应的值

示例代码:

+ 通过 [Storages.get()](/API/Storages/Storages/README.md?id=get)
  获取本地存储对象 [Storage](/API/Storages/Storage/README.md)
  ,并向其添加内容后通过 [Storage.get()](/API/Storages/Storage/README.md?id=get) 获取添加的内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()

// Storages.get() 用于获取本地存储对象 Storage
def storage = $storages.get('name')
// Storage.put() 用于向本地存储对象添加数据
storage.put('key1', 'value1')
storage.put('key2', 'value2')
// Storage.get() 用于根据key值获取本地存储对象中对应的值
$assert.assertTrue(storage.get('key1', null) == 'value1', '断言key1的值为value1')
$assert.assertTrue(storage.get('key2', null) == 'value2', '断言key2的值为value2')
```
