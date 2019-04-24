# 结构体 struct
结构体是一组不同类型变量的合集，需要实例化后才可使用，常用做描述对象。
一旦结构体被实例化，结构内所有的变量都会被赋与默认值。

声明：
```Go
//声明一个结构体类型
type A struct {
	b int
	c string
}
//实例化
var a A

//或者直接声明一个结构体变量
var a struct{
	b int
	c string
}
```

赋值：
```Go
//赋值
a.b=1
a.c="abc"
```

结构体组合：
```Go
type A struct {
    b int
    c string
}
type B struct {
    d int
    e string
}
type C struct {
    A   //组合结构体A
    B   //组合结构体B
}
```