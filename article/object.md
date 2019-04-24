# 定义对象
面向对象只是个概念，一个事物有属性和方法都可以称为对象。在Go中一般用`type`定义一个类型，再为这个类型赋与属性或方法，声明该类型的变量即可称为一个对象。

定义一个对象及其属性：
```Go
type Obj struct{
	Name string //定义对象的属性
}
```

定义Obj这个对象的方法Say()
```Go
func (o *Obj) Say() {
	log.Println(o.Name)
}
```

实例化一个对象
```Go
var obj Obj
//为对象的属性赋值
obj.Name = "龙青"
//执行对象的方法
obj.Say()
```