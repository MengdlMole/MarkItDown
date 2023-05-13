# 修改登录背景
## 使用脚本
```
wget -qO - https://github.com/PRATAP-KUMAR/ubuntu-gdm-set-background/archive/main.tar.gz | tar zx --strip-components=1 ubuntu-gdm-set-background-main/ubuntu-gdm-set-background
（也可以去github下载）
sudo ubuntu-gdm-set-background --image ~/Pictures/Prana.png
```
## 使用Tweaks
# 键盘Fn功能异常（MK870）
终端运行
```
echo 0 | sudo tee /sys/module/hid_apple/parameters/fnmode
```
参考
https://tieba.baidu.com/p/7767040599
https://mikeshade.com/posts/keychron-linux-function-keys/#:~:text=On%20Linux%2C%20the%20Keychron%20K2%20doesn%E2%80%99t%20register%20any,keyboard%20to%20Windows%20mode%20via%20the%20side%20switch


# 开放端口
## 防火墙配置
```
sudo ufw allow 22
sudo ufw allow 22/tcp
sudo ufw allow 22/udp
```
启动防火墙
```
sudo ufw enable
```
查看端口状态
```
sudo ufw status
sudo ufw status numbered
```

或者
```
netstat -a
netstat -anp |grep 22
```

删除端口
```
sudo ufw delete 1
sudo ufw delete 2
```

## ssh服务
```
sudo apt install openssh-server
sudo vim /etc/ssh/sshd_config
```
修改```#Port 22``` 可修改默认端口;

修改```#Gatewayports no``` 为```Gatewayports yes```;

查看ssh的状态：```sudo systemctl status ssh```;

防火墙设置```sudo ufw allow ssh```;

本机设置反向连接：```ssh -NRf 124.222.83.11:1037:localhost:8122 ubuntu@124.222.83.11```;

远程连接：```ssh username@ip```;

# 硬件设置
## 弹出硬盘
查看硬盘状态：``` sudo fdisk -l```;

弹出硬盘
```
udisksctl unmount -b /dev/sdb
udisksctl unmount -b /dev/sdb
```
