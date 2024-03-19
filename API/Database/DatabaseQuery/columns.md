功能:

+ 设置查询返回的列,如果不设置,默认返回所有列

定义:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) columns(List\<String\> columns)

参数:

+ List\<String\> columns - 需要返回的列

返回值:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [DatabaseQuery.columns()](/API/Database/DatabaseQuery/README.md?id=columns) 设置查询返回的列.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Databases.openOrCreateDatabase() 用于打开/创建数据库
def database = $databases.openOrCreateDatabase("M8Test_test.db")
// Database.createTable() 用于新建一个简单数据表,该表所有列均为text类型,并且存在自增id属性
database.createTable("user", ["username", "password"])
// Database.insert() 用于向数据表中插入数据
database.insert("user", null, ["username": "ZhangSan", "password": "123456"])
// Database.query() 用于查询数据库内容
def data = database.query {
    // delegate -> DatabaseQuery
    // DatabaseQuery.table() 用于设置需要查询的表名
    table("user")
    // DatabaseQuery.columns() 用于设置查询返回的列
    columns(["password"])
}
$assert.assertTrue(data.length() == 1, "数据大小为1")
def user = data.get(0)
// Exceptions.tryToRun() 用于执行异常代码,返回一个 Trier 对象
$exceptions.tryToRun {
    // 由于没有返回username对应的列,所以会抛异常
    def username = user.get("username")
    // 下面打印语句不会被执行
    $console.log(username)
}.catchAll {
    $console.log("username不存在")
}
$assert.assertTrue(user.get("password") == "123456", "密码")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```