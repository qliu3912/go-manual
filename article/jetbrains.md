# Jetbrains配置
使用Intellij IDEA、Goland等Jetbrains系的IDE配置Go开发环境：

1. 除了Goland之外都需要安装名为`go`的插件
2. 在软件设置中指定`GOROOT`的路径
3. 在软件设置中的`GOPATH`里找到`Project GOPATH`，将当前项目的路径添加进去，否则会无法导入项目内的自定义包。注意，这个设置是针对GOPATH特性的，与Modules特性冲突，建议新版本Go中不要设置此项。

打开`main.go`文件，点击`Run`按钮开始编译并调试代码。