# 类型断言
当一个值被"装箱"到interface再"拆箱"时需要断言成原本的类型才可以继续使用，有以下几种断言方式：

```Go
str := "abc"
s := str.(int)  //将str断言成int类型，这里肯定会失败
//由于上面断言失败，会触发panic错误，使用下面的写法更安全
s, ok := str.(int)
if ok == true {
	//断言成功，可以安全使用变量s的值
} else {
	//断言失败，变量s的值不可信
}
```

当不知道某个变量是什么类型的时候，可以用switch来尝试用不同的类型断言：
```Go
var s int = 123
var i interface{}
i = s

switch i.(type) {
case string:
    log.Println("string类型")
case int:
    log.Println("int类型")
//case ...:
default:
    log.Println("未知的类型，断言失败")
}
```