# GOBIN
`GOBIN`是指`{GOPATH}/bin`这个路径。使用`go env`命令可以查看该变量设置的值。

当用户通过`go get`命令下载某个源码包（例如goimports）时，系统会编译一个名为`goimports`的可执行文件存放在`{GOPATH}/bin`目录中。下载的源码在`GOPATH/src`目录。

为了方便开发，应该将`GOBIN`加入到系统的`PATH`变量中。