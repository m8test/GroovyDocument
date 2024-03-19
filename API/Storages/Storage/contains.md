功能:

+ 判断 [Storage](/API/Storages/Storage/README.md) 本地存储对象中是否存在指定键的键值对

定义:

+ boolean contains(String key)

参数:

+ String key - 需要判断是否存在于 [Storage](/API/Storages/Storage/README.md) 本地存储对象中的键

返回值:

+ boolean - 如果本地存储对象 [Storage](/API/Storages/Storage/README.md) 中存在该键对应的键值对返回true,否则返回false

示例代码:

+ 通过 [Storages.get()](/API/Storages/Storages/README.md?id=get)
  获取本地存储对象 [Storage](/API/Storages/Storage/README.md) ,并向其添加内容后通过
  [Storage.contains()](/API/Storages/Storage/README.md?id=contains) 判断本地存储对象中是否存在指定键对应的键值对.

```groovy

// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()

// Storages.get() 用于获取本地存储对象 Storage
def storage = $storages.get('name')
// Storage.put() 用于向本地存储对象添加数据
$assert.assertTrue(storage.put('key1', 'value1'))
$assert.assertTrue(storage.put('key2', 'value2'))
// Storage.contains() 用于判断本地存储对象中是否存在指定键对应的键值对
$assert.assertTrue(storage.contains('key1'), '断言本地存储对象中存在key1键值对')
$assert.assertTrue(storage.contains('key2'), '断言本地存储对象中存在key2键值对')
// Storage.remove() 用于移除本地存储对象中键对应的键值对
$assert.assertTrue(storage.remove('key1'))
$assert.assertTrue(storage.remove('key2'))
// Storage.contains() 用于判断本地存储对象中是否存在指定键对应的键值对
$assert.assertFalse(storage.contains('key1'), '断言本地存储对象中不存在key1键值对')
$assert.assertFalse(storage.contains('key2'), '断言本地存储对象中不存在key2键值对')
```