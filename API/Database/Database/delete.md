功能:

+ 根据条件删除数据表中的数据.

定义:

+ int delete(String table, String whereClause = null, List\<String\> whereArgs = null)

参数:

+ String table - 表名
+ String whereClause - where条件语句,例如 id=? or username=?
+ List\<String\> whereArgs - whereClause条件句中的参数,会将其中的?依次替换

返回值:

+ int - 如果传入whereClause参数,则返回受影响的行数,否则为0.如果要删除所有行并获得计数,whereClause参数请传"1"

示例代码:

+ 通过 [Database.delete()](/API/Database/Database/README.md?id=delete) 根据条件删除数据表中的数据.

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
def data = database.query { table("user") }
$assert.assertTrue(data.length() == 1, "数据大小为1")
def user = data.get(0)
$assert.assertTrue(user.get("username") == "ZhangSan", "用户名")
$assert.assertTrue(user.get("password") == "123456", "密码")
// Database.delete() 用于根据条件删除数据表中的数据.
$assert.assertTrue(database.delete("user", "id=? or username=?", ["1", "ZhangSan"]) == 1, "删除数据表数据成功")
// Database.delete() 用于根据条件删除数据表中的数据. whereClause 传 "1" 可以删除所有行并获得删除的行数
// $assert.assertTrue(database.delete("user", "1", null) == 1, "删除数据表数据成功")
// Database.query() 用于查询数据库内容
data = database.query { table("user") }
$assert.assertTrue(data.length() == 0, "数据大小为0")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```