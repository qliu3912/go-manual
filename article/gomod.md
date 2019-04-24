# go mod命令
`go mod`命令是在Go v1.11中加入的新命令，可以对项目进行模块化管理，用于替代原来的GOPATH包管理机制。

在使用GOPATH机制时，项目所有的源码必须位于GOPATH的src目录下。如果使用新的Module机制，则项目必须在GOPATH之外。

### go mod常用命令：
`go mod init demo`
<br>创建一个module，名为demo，之后在导入模块中的资源时，都以demo开头，例如`import demo/Var`

`go mod tidy`
<br>自动分析项目中Go源代码的依赖关系，并下载所依赖的模块代码到本地

`go mod vender`
<br>将依赖模块的代码保存到项目的`vender`目录中，但编译器并不从该目录搜索依赖。