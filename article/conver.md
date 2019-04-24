# 类型转换

强制类型转换失败会触发panic，在不能保证转换一定成功的时候尽量不要使用，或者配合recover()机制来确保进程安全。

int/int8/int16/int32/int64之间可以互相直接使用`<类型>()`强制转换，但高位向低位强制转换时如果值范围溢出会转换成-1，因此应该在转换前判断是否会溢出，例如：
```Go
import "math"

var i int64 = -1
//math.MaxInt32可以得到int32类型的最大值
if i > math.MaxInt32 {
    //不能安全转换到int32
} else {
    log.Println(int32(i))
}
```

string到int：
```Go
<string> = strconv.atoi(<string>, <int>)
```

string到[]byte：
```Go
<[]bytes> := []byte(<string>) 
```

string到int64
```Go
<string>, <error> = strconv.ParseInt(<string>, 10, 64)
```

string到float64
```Go
<float64>, <error> = strconv.ParseFloat(<string>, 10)
```

string到bool

能被转换成true的字符串"true"、"t"、"1"

能被转换成false的字符串"false"、"f"、"0"
```Go
<bool>, <error> = strconv.ParseBool(<string>)
```

int到string
```Go
<string> = strconv.itoa(<int>)
```

int到byte
```Go
<byte> = strconv.itoa(<int>)
```

int到float32/64
```Go
<float32> = float32(<int>)
<float64> = float64(<int>)
```

更多类型的转换待完善...