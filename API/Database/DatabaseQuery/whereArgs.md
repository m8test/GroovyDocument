功能:

+ 替换 [where](/API/Database/DatabaseQuery/README.md?id=where) 语句中的?

定义:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) whereArgs(List\<String\> whereArgs)

参数:

+ List\<String\> whereArgs - 替换?的数据

返回值:

+ [DatabaseQuery](/API/Database/DatabaseQuery/README.md) - 返回对象本身,方便链式调用

示例代码:

+ 通过 [DatabaseQuery.whereArgs()](/API/Database/DatabaseQuery/README.md?id=whereArgs)
  替换 [where](/API/Database/DatabaseQuery/README.md?id=where) 语句中的?

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
    // DatabaseQuery.where() 用于设置条件语句
    where("id = ?")
    // DatabaseQuery.whereArgs() 用于替换 where 语句中的?
    whereArgs(["2"])
}
$assert.assertTrue(data.length() == 1, "数据大小为1")
def user = data.get(0)
$assert.assertTrue(user.get("username") == "LiSi", "用户名")
$assert.assertTrue(user.get("password") == "123456", "密码")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```