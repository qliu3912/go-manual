# 函数析构
在Go中，析构被深入到了函数，通过`defer`关键字使函数在return时执行执定的逻辑，例如：

```Go
func main() {
	s := ""

	defer func() {
		println(s)
		s += ",我最后执行"
		println(s)
	}()

	defer func() {
		s = "我先执行"
	}()
}
```

以上代码通过defer定义了两个函数析构逻辑，在函数正常退出时执行两个匿名函数，defer触发的顺序是从下往上，即最先定义的最后执行。
##### 注意：执行了log.Fatal()、panic()等原因造成的非正常退出，defer将无法触发。