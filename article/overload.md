# 多对象组合
在组合两个对象时，如果两个对象中有同名的方法存在，则会导致被组合对象的同名方法被重载。

示例：
```Go
//定义两个对象
type A struct {
	Name string
}
type B struct {
	A             //组合对象A
	Gender string
}

//定义对象A的方法，打印自己的Name属性
func (a *A) SayName() {
	println("对象A：", a.Name)
}

//定义对象B的方法跟A的方法相同，但打印自己的Gender属性，实现重载
func (b *B) SayName() {
	println("对象B：", b.Gender)
}

func main() {
	//实例化对象B
	var obj B
	//为对象的属性赋值
	obj.Name = "龙青"
	obj.Gender = "男"
	//执行对象的方法，最终执行的是对象B的方法
	obj.SayName()
}
```