# 对象接口
使用interface{}定义一个接口以及方法，如果某个对象实现了接口中的方法，则认为实现了该接口。

```Go
//定义一个"动物"接口类型
type Animal interface {
	Say()
}

//定义一个"狗"
type Dog struct {
	Name string
}

//为"狗"定义Say()方法，实现了Animal接口
func (d *Dog) Say() {
	println(d.Name)
}

//定义一个"猫"
type Cat struct {
	Name string
}

//为"猫"定义Say()方法，也实现了Animal接口
func (d *Cat) Say() {
	println(d.Name)
}

func main() {
	//实例化一只狗
	var dog Dog
	dog.Name = "我是史努比"
	//实例化一只猫
	var cat Cat
	cat.Name = "我是汤姆"

	//把狗送进动物园
	zoo(&dog)
	//把猫送进动物园
	zoo(&cat)
}

//定义一个函数叫"动物园"，接受传入各种名称的"动物"
//由于"狗"和"猫"并不是一个类型，所以需要这两个类型都实现"动物"这同一个接口
//这样才能把不同的类型都传入"动物园"这个函数中
func zoo(obj Animal) {
	obj.Say()
}
```