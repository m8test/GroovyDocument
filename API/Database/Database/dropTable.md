功能:

+ 删除数据表.

定义:

+ boolean dropTable(String table)

参数:

+ String table - 表名

返回值:

+ boolean - 如果删除数据表成功返回true,否则返回false

示例代码:

+ 通过 [Database.dropTable()](/API/Database/Database/README.md?id=dropTable) 删除数据表.

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
// Database.dropTable() 用于删除数据表
$assert.assertTrue(database.dropTable("user"), "删除数据表")
// Database.dropTable() 用于删除数据表,第二次删除返回false
$assert.assertFalse(database.dropTable("user"), "第二次删除数据表")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```