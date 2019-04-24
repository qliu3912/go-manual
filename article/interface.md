# 接口 interface
interface有多种用途，可以模拟泛型，也可以在面向对象概念中当做接口使用。
当做泛型使用时可以赋值任何类型的值，但不能直接与其它类型比较，需要断言成一个新的变量才可使用。可以形象的理解为赋值到interface里是装箱操作，从interface里取出来断言是拆箱操作。

默认值nil

声明：
```Go
var i interface{}
```

当做泛型使用：
```Go
//声明一个字符串
var s string = "abc"
//声明一个interface
var i interface{}

//把string类型赋值给interface，装箱
i = s

//把i断言成string类型，拆箱
ss := i.(string)
s += ss
log.Println(s)
```

点击此处查看当做接口使用的方法