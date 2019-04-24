# 错误 error
error类型本质上是一个interface类型，专用于表示出现错误，默认值为nil。

赋值方法：
```Go
import "errors"
err := errors.New("错误消息")
```

获得字符串类型的消息：
```Go
err := errors.New("错误消息")
log.Println(err.Errors())
```