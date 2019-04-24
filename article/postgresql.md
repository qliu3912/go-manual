# PostgreSQL 操作
使用[github.com/go-pg/pg](https://github.com/go-pg/pg)包连接PostgreSQL数据库

go-pg包可以通过预先定义好的模型`Model(&struct)`来用`Insert()`、`Select()`、`Update()`、`Delete()`等方法操作数据

也可以直执行SQL语句`Query()`、`QueryOne()`、`Exec()`、`ExecOne()`

#### 连接数据库
```Go
import (
	"time"

	"github.com/go-pg/pg"
)

//数据库连接实例（内含连接池，可以做为全局变量使用，不用担心并发安全问题）
var DB *pg.DB

//定义User表模型
type User struct {
	tableName struct{} `sql:"user"`     //表名
	ID        int64    `sql:"id"`       //id字段
	Username  string   `sql:"username"` //username字段
	Password  string   `sql:"password"` //password字段
}

func main() {
	//创建一个连接配置实例
	var option pg.Options
	option.Addr = "192.168.1.240:5432"    //连接地址
	option.User = "postgres"              //连接账号
	option.Password = "a2b4c6"            //连接密码
	option.Database = "mytest"            //数据库名
	option.DialTimeout = 5 * time.Second  //连接超时（5秒）
	option.ReadTimeout = 5 * time.Second  //读超时（5秒）
	option.WriteTimeout = 5 * time.Second //写超时（5秒
	//连接数据库
	DB = pg.Connect(&option)
	//打印查询语句
	DB.OnQueryProcessed(func(event *pg.QueryProcessedEvent) {
		query, err := event.FormattedQuery()
		if err != nil {
			println(err.Error())
			return
		}
		println("[SQL] ", time.Since(event.StartTime).String(), " | ", query)
	})

	//插入记录
	id, err := insert("user1", "111111")
	if err != nil {
		return
	}
	//用事务插入多条记录
	insertMulti()
	//查询单条记录
	query(id)
	//更新记录
	update(id)
	//再次查询那条记录
	query(id)
	//查询所有记录
	queryMulti()
	//删除记录
	delete(id)
}

//插入记录
func insert(username, password string) (int64, error) {
	println("【插入记录】")
	//定义一个变量用于保存新插入记录的ID
	var ID int64
	//实例化一个模型
	var user User
	user.ID = time.Now().Unix() //赋值ID字段，生产环境不可以用时间戳做主键
	user.Username = username    //赋值username字段
	user.Password = password    //赋值password字段

	//插入记录
	result, err := DB.Model(&user).Returning("id").Insert(&ID)
	if err != nil {
		println(err.Error())
		return 0, err
	}
	println("插入了", result.RowsAffected(), "条记录")
	println("最新插入的记录ID：", ID)
	return ID, nil
}

//用事务插入多条记录
func insertMulti() {
	println("【插入多条记录】")
	//启用事件
	tx, err := DB.Begin()
	if err != nil {
		println(err.Error())
		return
	}
	//函数退出时回滚事务（不会将已经commit的数据回滚)
	defer tx.Rollback()

	//实例化一个模型
	var user User
	user.ID = time.Now().Unix() + 1 //赋值ID字段，生产环境不可以用时间戳做主键
	user.Username = "dxvgef1"       //赋值username字段
	user.Password = "123456"        //赋值password字段
	//插入记录
	_, err = DB.Model(&user).Insert()
	if err != nil {
		println(err.Error())
		return
	}

	//重新赋值user对象
	user.ID = time.Now().Unix() + 2
	user.Username = "dxvgef2"
	user.Password = "1233457"
	//插入记录
	_, err = DB.Model(&user).Insert()
	if err != nil {
		println(err.Error())
		return
	}

	//提交事务
	err = tx.Commit()
	if err != nil {
		println(err.Error())
		return
	}
}

//查询单条记录
func query(ID int64) {
	println("【查询一条记录】")
	//假设只有一条记录
	var user User
	//查询记录
	err := DB.Model(&user).Where("id=?", ID).Select()
	if err != nil {
		println(err.Error())
		return
	}

	println("id:", user.ID)
	println("username:", user.Username)
	println("password:", user.Password)
}

//查询多条记录
func queryMulti() {
	println("【查询多条记录】")
	//假设有多条记录
	var users []User
	//查询记录
	err := DB.Model(&users).Select()
	if err != nil {
		println(err.Error())
		return
	}
	println("取得了", len(users), "条记录")

	//遍历记录
	for k := range users {
		println("id:", users[k].ID)
		println("username:", users[k].Username)
		println("password:", users[k].Password)
	}
}

//修改记录
func update(id int64) {
	println("【更新记录】")
	result, err := DB.Model(&User{}).Set("username=?", "龙青").Where("id=?", id).Update()
	if err != nil {
		println(err.Error())
		return
	}
	println("更新成功，影响了", result.RowsAffected(), "条记录")
}

//删除记录
func delete(id int64) {
	println("【删除记录】")
	result, err := DB.Model(&User{}).Where("id=?", id).Delete()
	if err != nil {
		println(err.Error())
		return
	}
	println("删除了", result.RowsAffected(), "条记录")
}
```