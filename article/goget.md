# go get命令
`go get `命令可以通过git下载远程git服务器上的源码包到本地`GOPATH/src`目录中，例如：

`go get github.com/dxvgef/tsing`

下载完成后的存放路径：

`GOPATH/src/github.com/dxvgef/tsing`

由于Go的编译器会自动查找`GOPATH`的`src`目录，所以在源码中导入这个包时可以直接写：

```
import "github.com/dxvgef/tsing"
```