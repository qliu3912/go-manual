# 映射 map
map类型是一个Hash表，以Key/Value关系存储，因此需要用`make()`来分配初始的内存空间：
默认值：map[]，可用nil来判断是否为空

##### 定义
```Go
//定义一个key和value都是string类型的map
m := make(map[string]string)

//定义一个key是string，value是int类型的map
m2 := make(map[string]int)

//定义一个值可能存任何类型的map，但访问该值时需要自行断言
m3 := make(map[string]interface{})
```

##### 访问
```Go
m["a"]="1"
m2["a"]=1
m3["a"]=false
```