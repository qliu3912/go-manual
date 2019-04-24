# 字符串
string类型可以使用双引号""表示单行字符串，也可以使用``表示多行字符串。

字符串拼接使用+号。

string类型可以转换为[]byte类型得到每个字符的ASCII码。

默认值：""

如果要判断可能含有汉字的字符串长度，应该使用以下方法：
```
import "unicode/utf8"
utf8.RuneCountInString("中国china")
```

字符串可以使用[切片](./slice.md)操作，例如：
```Go
str := "abcdefg"
str[3:]
```