功能:

+ 设置查询结果是否去重.

定义:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) distinct(boolean distinct)

参数:

+ boolean distinct - 如果希望每一行都是唯一的，则为true，否则为false。

返回值:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [DatabaseQuery.distinct()](/API/Database/DatabaseQuery/README.md?id=distinct) 设置查询结果是否去重.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Databases.openOrCreateDatabase() 用于打开/创建数据库
def database = $databases.openOrCreateDatabase("M8Test_test.db")
// Database.createTable() 用于新建一个简单数据表,该表所有列均为text类型,并且存在自增id属性
database.createTable("user", ["username", "password"])
// Database.insert() 用于向数据表中插入数据,插入两条相同的数据
database.insert("user", null, ["username": "ZhangSan", "password": "123456"])
database.insert("user", null, ["username": "ZhangSan", "password": "123456"])
// Database.query() 用于查询数据库内容
def data = database.query {
    // delegate -> DatabaseQuery
    // DatabaseQuery.table() 用于设置需要查询的表名
    table("user")
    // DatabaseQuery.columns() 用于设置查询返回的列,由于默认有id属性,并且其唯一,所以在此去除id属性,这样数据库中的两条数据就是相同的了,也就是重复了,所以去重之后只有一条数据
    columns(["username", "password"])
    // DatabaseQuery.distinct() 用于设置查询结果是否去重.
    distinct(true)
}
$assert.assertTrue(data.length() == 1, "数据大小为1")
def user = data.get(0)
$assert.assertTrue(user.get("username") == "ZhangSan", "用户名")
$assert.assertTrue(user.get("password") == "123456", "密码")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```