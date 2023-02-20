# vscode 配置 FreeFem++
1. 搜索并安装 FreeFem++ 相应的语法插件；
2. 配置 launch.json 文件以便调试：
    点击 运行>添加launch.json文件 ， 之后可选择 C++(Windows) （或其他合适的配置文件） ，并配置FreeFem++执行文件的路径，具体配置如下：
    ```
    {
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(Windows) 启动",
            "type": "cppvsdbg",
            "request": "launch",
            "program": "D:/CodeDevelopment/FreeFem++/FreeFem++.exe",
            "args": [
                "-f",
                "${file}"
            ],
            "stopAtEntry": false,
            "cwd": "D:/CodeDevelopment/FreeFem++",
            "environment": [],
            "console": "externalTerminal"
        }
    ]
    }
    ```
