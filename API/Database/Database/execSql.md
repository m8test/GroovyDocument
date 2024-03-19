功能:

+ 执行一条不是SELECT的SQL语句或任何其他返回数据的SQL语句。

定义:

+ boolean execSql(String sql)

参数:

+ String sql - 需要执行的sql语句

返回值:

+ boolean - 如果执行sql成功返回true,否则返回false

示例代码:

+ 通过 [Database.execSql()](/API/Database/Database/README.md?id=execSql) 创建数据表.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// Databases.openOrCreateDatabase() 用于打开/创建数据库
def database = $databases.openOrCreateDatabase("M8Test_test.db")
// Database.execSql() 用于执行sql语句
database.execSql("create table user(id integer primary key autoincrement, username text, password text)")
// Database.insert() 用于向数据表中插入数据
database.insert("user", null, ["username": "ZhangSan", "password": "123456"])
// Database.query() 用于查询数据库内容
def data = database.query { table("user") }
$assert.assertTrue(data.length() == 1, "数据大小为1")
def user = data.get(0)
$assert.assertTrue(user.get("id") == 1, "用户ID")
$assert.assertTrue(user.get("username") == "ZhangSan", "用户名")
$assert.assertTrue(user.get("password") == "123456", "密码")
// Databases.dropDatabase() 用于删除数据库
$assert.assertTrue($databases.dropDatabase(database), "删除数据库")
```