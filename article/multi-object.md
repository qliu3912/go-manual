# 多对象组合
在Go中没有对象继承这个概念，当一个对象要拥有另一个对象的属性和方法时，可以组合两个对象

定义两个对象及其属性：
```Go
//定义两个对象
type A struct {
	Name string //定义对象的属性
}
type B struct {
	A             //组合对象A
	Gender string //定义对象的属性
}

//定义对象A的方法
func (a *A) SayName() {
	log.Println(a.Name)
}

//定义对象B的方法
func (b *B) SayGender() {
	log.Println(b.Gender)
}

func main() {
	//实例化对象B
	var obj B
	//为对象的属性赋值
	obj.Name = "龙青"  //这是从对象A组合来的Name属性
	obj.Gender = "男" //这是自己原有的属性
	//执行对象的方法
	obj.SayName()   //这是从对象A组合来的方法
	obj.SayGender() //这是自己原有的方法
}
```