功能:

+ 更新数据库内容.

定义:

+ int update(String table, Map<String, Object> values, String whereClause = null, List\<String\>
  whereArgs = null)

参数:

+ String table - 表名
+ Map<String, Object> values - 需要更新的数据,键值对形式,键为需要更新的列名,值为需要更新的值
+ String whereClause - 条件语句,可以带有?
+ List\<String\> whereArgs - whereClause条件句中的参数,会将其中的?依次替换

返回值:

+ int - 受影响的行数(更新的行数)

示例代码:

+ 通过 [Database.update()](/API/Database/Database/README.md?id=update) 更新数据库内容.

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
// Database.update() 用于更新数据库内容
$assert.assertTrue(database.update("user", ["username": "LiSi"], "id = ? and username = ?", ["1", "ZhangSan"]) == 1, "更新数据")
// Database.rawQuery() 用于使用sql查询数据库内容.
data = database.rawQuery("select * from user ")
$assert.assertTrue(data.get(0).get("username") == "LiSi", "更新后的用户名")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```