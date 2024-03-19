功能:

+ 使用sql查询数据库内容.

定义:

+ [JSONArray](/API/Json/JSONArray/README.md) rawQuery(String sql, List\<String\> selectionArgs = null)

参数:

+ String sql - 查询sql语句,条件可使用可用?,例如 id=? or username=?
+ List\<String\> selectionArgs - 用于依次替换sql中的?,可以为null(默认值,sql中没有?)

返回值:

+ [JSONArray](/API/Json/JSONArray/README.md) - 根据条件查询到的结果.

示例代码:

+ 通过 [Database.rawQuery()](/API/Database/Database/README.md?id=rawQuery) 使用sql查询数据库内容.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Databases.openOrCreateDatabase() 用于打开/创建数据库
def database = $databases.openOrCreateDatabase("M8Test_test.db")
// Database.createTable() 用于新建一个简单数据表,该表所有列均为text类型,并且存在自增id属性
database.createTable("user", ["username", "password"])
// Database.insert() 用于向数据表中插入数据
$assert.assertTrue(database.insert("user", null, ["username": "ZhangSan", "password": "123456"]) == 1, "插入行ID为1")
// Database.rawQuery() 用于使用sql查询数据库内容.
def data = database.rawQuery("select * from user where id=? and username=?", ["1", "ZhangSan"])
$assert.assertTrue(data.length() == 1, "数据大小为1")
def user = data.get(0)
$assert.assertTrue(user.get("username") == "ZhangSan", "用户名")
$assert.assertTrue(user.get("password") == "123456", "密码")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```