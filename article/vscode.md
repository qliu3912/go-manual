# VS Code配置
1. 在VS Code中安装Go扩展
2. 打开一个Go源码文件，安装所有VS Code提示要安装的扩展
3. 修改VS Code的`用户设置`配置文件：
```
"go.formatTool": "goimports",
"go.goroot": "改为GOROOT路径",
"go.gocodeAutoBuild": false,
"go.gopath": "改为GOPATH路径",
"go.autocompleteUnimportedPackages": true,
"go.useCodeSnippetsOnFunctionSuggest": true,
"go.useCodeSnippetsOnFunctionSuggestWithoutType": true,
"go.gotoSymbol.includeImports": true,
```
4. 修改工作区配置文件`.vscode/setting.json`：
```
{
  "go.gopath": "${workspaceRoot}:GOPATH的路径"
}
```
5. 修改调试配置文件`.vscode/launch.json`文件：
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch",
            "type": "go",
            "request": "launch",
            "mode": "debug",
            "remotePath": "",
            "port": 2345,
            "host": "127.0.0.1",
            "program": "${workspaceRoot}/src/main/main.go",
            "cwd": "${workspaceRoot}",
            "env": {
                "GOPATH": "${workspaceRoot}:GOPATH的路径"
            },
            "args": [],
            "showLog": true
        }
    ]
}
```
启动VS Code的调试功能开始编译调试代码，调试时编译的文件会创建在`${workspaceRoot}/src/main/`目录中，文件名为`debug`