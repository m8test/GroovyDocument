功能:

+ 设置查询结果排序方式

定义:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) orderBy(String orderBy)

参数:

+ String orderBy - 排序方式

返回值:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [DatabaseQuery.orderBy()](/API/Database/DatabaseQuery/README.md?id=orderBy) 设置查询结果排序方式

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Databases.openOrCreateDatabase() 用于打开/创建数据库
def database = $databases.openOrCreateDatabase("M8Test_test.db")
// Database.createTable() 用于新建一个简单数据表,该表所有列均为text类型,并且存在自增id属性
database.createTable("user", ["username", "password"])
// Database.insert() 用于向数据表中插入数据
database.insert("user", null, ["username": "ZhangSan", "password": "123456"])
database.insert("user", null, ["username": "LiSi", "password": "123456"])
database.insert("user", null, ["username": "WangWu", "password": "123456"])
// Database.query() 用于查询数据库内容
def data = database.query {
    // delegate -> DatabaseQuery
    // DatabaseQuery.table() 用于设置需要查询的表名
    table("user")
    // DatabaseQuery.orderBy() 用于设置查询结果排序方式
    orderBy("id desc")
}
$assert.assertTrue(data.length() == 3, "数据大小为3")
// id降序,所以第一个结果id为3也就是username为WangWu
def user = data.get(0)
$assert.assertTrue(user.get("username") == "WangWu", "用户名")
$assert.assertTrue(user.get("password") == "123456", "密码")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```