# 自定义函数
自定义函数使用`func`关键字。

Go中的函数支持可变入参，不支持可变出参，但支持返回多个出参

只有一个出参：
```Go
func 函数名(入参1 string, 入参2 int) string {
	return ""
}
```

提前为出参定义好变量名：
```Go
func 函数名(入参1 string, 入参2 int) (出参1 string) {
	出参1="test"
	return
}
```

两个出参：
```Go
func 函数名(入参1 string, 入参2 int) (string, error) {
	return "", nil
}
```