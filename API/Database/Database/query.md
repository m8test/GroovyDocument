功能:

+ 查询数据库内容.

定义:

+ [JSONArray](/API/Json/JSONArray/README.md) query(Closure closure)

参数:

+ Closure closure - 设置查询参数的闭包
    + 参数 - 无
    + delegate - [DatabaseQuery](/API/Database/DatabaseQuery/README.md)

返回值:

+ [JSONArray](/API/Json/JSONArray/README.md) - 根据条件查询到的结果.

示例代码:

+ 通过 [Database.query()](/API/Database/Database/README.md?id=query) 查询数据库内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Databases.openOrCreateDatabase() 用于打开/创建数据库
def database = $databases.openOrCreateDatabase("M8Test_test.db")
// Database.createTable() 用于新建一个简单数据表,该表所有列均为text类型,并且存在自增id属性
database.createTable("user", ["username", "password"])
// Database.insert() 用于向数据表中插入数据
$assert.assertTrue(database.insert("user", null, ["username": "ZhangSan", "password": "123456"]) == 1, "插入行ID为1")
// Database.query() 用于查询数据库内容
def data = database.query {
    // delegate -> DatabaseQuery
    // DatabaseQuery.table() 用于设置需要查询的表名
    table("user")
}
$assert.assertTrue(data.length() == 1, "数据大小为1")
def user = data.get(0)
$assert.assertTrue(user.get("username") == "ZhangSan", "用户名")
$assert.assertTrue(user.get("password") == "123456", "密码")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```