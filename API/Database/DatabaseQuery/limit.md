功能:

+ 限制查询返回的行数

定义:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) limit(String limit)

参数:

+ String limit - 限制查询返回的行数，格式为LIMIT子句。传递null表示没有LIMIT子句。

返回值:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [DatabaseQuery.limit()](/API/Database/DatabaseQuery/README.md?id=limit) 限制查询返回的行数.

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
    // DatabaseQuery.limit() 用于限制查询返回的行数
    limit("2")
}
$assert.assertTrue(data.length() == 2, "数据大小为2")
def user = data.get(0)
$assert.assertTrue(user.get("username") == "ZhangSan", "用户名1")
$assert.assertTrue(user.get("password") == "123456", "密码1")
user = data.get(1)
$assert.assertTrue(user.get("username") == "LiSi", "用户名2")
$assert.assertTrue(user.get("password") == "123456", "密码2")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```