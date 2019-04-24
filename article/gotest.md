# go Test命令
`go test`命令可以运行Go的单元测试源码文件，例如：

```
//demo.go
func show(str string) string {
    return str
}
```

```
//demo_test.go
//单元测试文件以_test结尾，下划线前与要测试的源码文件名相同

//导入testing包
import "testing"

//执行测试的函数以Test开头
func TestShow(t *testing.T) {
    t.Println(show())
}
```

建立以上两个源码文件后，运行以下命令查看测试结果：

`go test demo.go demo_test.go`