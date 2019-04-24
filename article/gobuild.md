# go build命令
`go build`命令编译指定的包或者源码文件，如果不指定包名则默认编译名为`main`的包：

以下命令将`main.go`中的代码编译成`test.exe`文件
```
go build main -o test.exe main.go
```

如果需要跨平台编译，需在执行`go build`前自行用命令更改`GOOS`等系统变量。