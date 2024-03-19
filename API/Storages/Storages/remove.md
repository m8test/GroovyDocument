功能:

+ 根据名称删除 [Storage](/API/Storages/Storage/README.md) 本地存储对象中的所有内容.

定义:

+ boolean remove(String name)

参数:

+ String name - 被删除内容的 [Storage](/API/Storages/Storage/README.md) 本地存储的名称

返回值:

+ boolean - 删除成功返回true,否则返回false

示例代码:

+ 通过 [Storages.get()](/API/Storages/Storages/README.md?id=get)
  获取本地存储对象 [Storage](/API/Storages/Storage/README.md) ,并向其添加内容后再通过
  [Storages.remove()](/API/Storages/Storages/README.md?id=remove)
  删除 [Storage](/API/Storages/Storage/README.md) 本地存储对象中的内容.

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
// Storage.remove() 用于删除名称对应的本地存储对象中的内容
$assert.assertTrue($storages.remove('name'), '删除本地存储对象内容')
// Storage.get() 用于根据key值获取本地存储对象中对应的值
$assert.assertTrue(storage.get('key1') == null, '断言key1的值为null')
$assert.assertTrue(storage.get('key2') == null, '断言key2的值为null')
```