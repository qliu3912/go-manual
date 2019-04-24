# 指针
使用`*`符号表示定义的是指针类型

使用`**`符号表示访问一个指针指向地址的值

使用`&`符号表示访问一个变量的指针
```Go
	var i *int      //定义一个指针类型，它只能指向到int类型的地址
	var j int = 10  //定义一个int类型的普通变量并赋值为10
	i = &j          //用&符号访问变量j的指针地址，并将地址赋值给i
	log.Println(i)  //打印i得到的是i这个指针的地址
	log.Println(*i) //在一个指针类型的变量前面再加一个*，即可得到该指针指向的地址中的值
	log.Println(j)  //打印j得到的是j的值
```

如果要在函数内外传递一个结构体，仅传递该结构体的指针地址而非拷贝，可以减少内存占用及分配开销：
```Go
type Obj struct {
	Name string
}

func main() {
	//实例化一个对象
	var obj Obj

	processCopy(obj)            //将对象的拷贝传入函数
	println("name:" + obj.Name) //打印出来为空，因为函数影响的是它的拷贝体

	processPointer(&obj)        //将对象的指针传入函数
	println("name:" + obj.Name) //打印出来了，说明函数影响到了它本身
}

//传入对象的指针，为原始对象的属性赋值
func processPointer(o *Obj) {
	o.Name = "龙青"
}

//传入对象的拷贝，为拷贝对象的属性赋值
func processCopy(o Obj) {
	o.Name = "龙青的拷贝"
}
```