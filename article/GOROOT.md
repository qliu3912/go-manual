# GOROOT
`GOROOT`是指go的安装路径，必须在系统环境变量中设置`GOROOT`，否则无法调试编译go源码。非源码安装的Go都会自动设置`GOROOT`。

当执行`go run`、`go build`等命令时，系统需要从`{GOROOT}/bin/`目录开始找这些命令的可执行文件。

使用`go env`命令可以查看该变量设置的值。

##### 例如：
【Windows】

将下载的go源码包解压在`C:\apps\go`里，则必须在Windows系统的环境变量里设置`GOROOT`变量的值为`C:\apps\go`

【Linux/Mac OS/...】

将下载的go源码包解压在`/apps/go`里，则必须在Shell的环境变量里设置`GOROOT`变量的值为`/apps/go`