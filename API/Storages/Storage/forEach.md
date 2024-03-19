功能:

+ 遍历 [Storage](/API/Storages/Storage/README.md) 本地存储对象中所有的键值对.

定义:

+ [Storage](/API/Storages/Storage/README.md) forEach(Closure closure)

参数:

+ Closure closure - 包含键值对的闭包对象
    + 参数
        + String key - 键
        + String value - 值
    + delegate - 无

返回值:

+ [Storage](/API/Storages/Storage/README.md) - 返回对象本身方便链式调用

示例代码:

+ 通过 [Storages.get()](/API/Storages/Storages/README.md?id=get)
  获取本地存储对象 [Storage](/API/Storages/Storage/README.md)
  ,并向其添加内容后通过 [Storage.forEach()](/API/Storages/Storage/README.md?id=forEach) 遍历添加的内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()

// Storages.get() 用于获取本地存储对象 Storage
def storage = $storages.get('name')
// Storage.put() 用于向本地存储对象添加数据
$assert.assertTrue(storage.put('key1', 'value1'))
$assert.assertTrue(storage.put('key2', 'value2'))
// Storage.forEach() 用于遍历本地存储对象中所有的键值对
storage.forEach { String key, String value ->
    if (key == 'key1') {
        $assert.assertTrue(value == 'value1', '断言key1的值为value1')
    } else if (key == 'key2') {
        $assert.assertTrue(value == 'value2', '断言key2的值为value2')
    }
}
```