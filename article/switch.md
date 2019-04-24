# switch
Go中的switch可以不需要在每个case中写break，但写上break也不会报错。
而且在写case的值时，可以执行一个函数获得其返回值来做为条件。

示例：
```Go
str := "1"
switch str {
case strconv.Itoa(len(str)):
    //获得str的长度的string类型
    //条件成立
case "1":
    //条件成立
default:
    //默认情况处理
}
```