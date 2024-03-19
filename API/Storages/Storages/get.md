功能:

+ 根据名称获取 [Storage](/API/Storages/Storage/README.md) 本地存储对象.

定义:

+ Storage get(String name)

参数:

+ String name - [Storage](/API/Storages/Storage/README.md) 本地存储的名称

返回值:

+ [Storage](/API/Storages/Storage/README.md) - 与参数 name 对应的本地存储对象

示例代码:

+ 通过 [Storages.get()](/API/Storages/Storages/README.md?id=get)
  获取本地存储对象 [Storage](/API/Storages/Storage/README.md) ,并向其添加内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()

// Storages.get() 用于获取本地存储对象 Storage
def storage = $storages.get('name')
// Storage.put() 用于向本地存储对象添加数据
storage.put('key1', 'value1')
storage.put('key2', 'value2')
// Storage.get() 用于根据key值获取本地存储对象中对应的值
$assert.assertTrue(storage.get('key1') == 'value1', '断言key1的值为value1')
$assert.assertTrue(storage.get('key2') == 'value2', '断言key2的值为value2')
```