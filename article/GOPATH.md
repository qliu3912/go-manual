# GOPATH
## 注意，新版本已支持modules，建议不要再使用GOPATH机制，并且Go之后的版本将移除GOPATH的支持
`GOPATH`是用于存放使用`go get`命令下载的第三方包源代码的路径。使用`go env`命令可以查看该变量设置的值。

在编译Go源代码时，编译器分析源代码中导入的包，以`{GOPATH}/src`为根路径往下查找包的源代码。

由于Go语言的vendor特性要求`vendor`目录必须放在`GOPATH`下面，导致项目的源代码也必须放在`GOPATH`中。

以Windows系统为例，假设`GOROOT`是`C:\apps\go\`，`GOPATH`是`E:\go-project\`，要编译以下代码：
``` Go
import (
    "log"
    "github.com/dxvgef/tsing"
)
```
编译器会从以下目录查找`log`包和`httpdispacher`包的源代码：
```
C:\apps\go\src\log  //命中
E:\go-project\src\log
C:\apps\go\src\github.com\dxvgef\tsing
E:\go-project\src\github.com\dxvgef\tsing  //命中
```
##### 注意，编译器只会从名为`src`的目录查找包的源代码。

`GOPATH`下面会自动生成`pkg`、`src`、`bin`三个子目录。
* `pkg`目录是存放编译好的第三方链接库
* `src`目录是存放第三方源代码
* `bin`目录是存放第三方工具可执行文件