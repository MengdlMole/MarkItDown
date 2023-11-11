# 这是一个配置code-server的教程

## code-server for linux

### 下载code-server

```通过终端下载
curl -fsSL https://code-server.dev/install.sh | sh
```

### 开启服务

```开启服务
sudo sysremctl start code-server@username % code-server，启动！
sudo sysremctl restart code-server@username % code-server，重启！
sudo sysremctl enable code-server@username % 开机自启
```

### 设置配置文件

```设置配置文件
vim ~/.config/code-server/config.yaml
```

```内容如下
bind-addr: 0.0.0.0:8080
auth: password
password: yourpassword
cert: false
```

### 扩展插件路径

```扩展插件路径
~/.local/share/code-server/extensions % code-server扩展插件路径
~/.vscode/extensions % vscode扩展插件路径
~/.vscode-server/extensions % 不记得这是什么的路径了
```

### 开放端口

```开放端口
ufw status
ufw allow 8080
ufw reload
```

## code-server for windows

### 通过npm下载

#### 下载nodejs

code-server官方文档： [https://coder.com/docs/code-server/latest/npm]

GitHub下载指定版本的nodejs: [https://github.com/nodejs/release]

#### 配置nodejs

```更换镜像源（可选）
npm config set registry https://registry.npm.taobao.org
```

```更换npm默认shell（windows默认shell无法执行.sh文件）
npm config set script-shell "C:\Program Files\Git\bin\bash.exe" % 自行修改为自己的路径
```

```修改npm安装路径
npm config set prefix "***\nodejs\node_global"
npm config set cache "***\nodejs\node_cache"
% 修改环境变量
% 新建系统变量NODE_HOME
% 新建Path变量%NODE_HOME%
% 新建Path变量%NODE_HOME%\node_modules
% 新建Path变量%NODE_HOME%\node_global
```

#### 安装code-server

```安装code-server
% 新建文件夹code-server
cd ***/code-server
npm install --global code-server --unsafe-perm
```

#### 配置code-server

```启动以初始化
code-server
```

```设置配置文件
C:\Users\AppData\Roaming\code-server\Config\config.yaml
```

```扩展插件路径
C:\Users\AppData\local\code-server\extensions % code-server扩展插件路径
C:\Users\AppData\.vscode\extensions % vscode扩展插件路径
```
