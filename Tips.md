## Shell 获取目录下的所有目录

```
for dir in `ls -d */`;do
	ls -lh $dir
done
```



## CentOS 网络相关

1. 配置网卡

   vi /etc/sysconfig/network-scripts/ifcfg-enp0s10

   > dhcp

   ```
   TYPE=Ethernet
   BOOTPROTO=dhcp
   DEVICE=enp0s10
   ONBOOT=yes
   ```

   > static

   ```
   TYPE=Ethernet
   BOOTPROTO=static
   IPADDr=192.168.56.1
   PREFIX=24
   DEVICE=enp0s10
   ONBOOT=yes
   ```

   

1. 

## VirtualBox 常用命令

1. Headless start

   > VBoxManage startvm <uuid|vmname> [--type gui|headless|separate]

1. Pause/Resume

   > VBoxManage controlvm <uuid|vmname> pause|resume|poweroff|savestate|reset

1. 查看vm信息

   > VBoxManage showvminfo <uuid|vmname> [--details]

1. 控制Guest

   > TODO VBoxManage guestcontrol 

## Mac: smart quotes and dashes

> 会把2个英文短横变成1个中文长横
>
> 关闭方法：System Preferences -> Keyboard -> Text -> uncheck "Use smart quotes and dashes"

## Docker: enable the remote API for dockerd

1. TODO use TLS to secure the deamon

2. Create a file at `/etc/systemd/system/docker.service.d/startup_options.conf` with the below contents:

   ```
   # /etc/systemd/system/docker.service.d/override.conf
   [Service]
   ExecStart=
   ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2376
   ```

   > **Note:** The -H flag binds dockerd to a listening socket, either a Unix socket or a TCP port. You can specify multiple -H flags to bind to multiple sockets/ports. The default -H fd:// uses systemd's socket activation feature to refer to /lib/systemd/system/docker.socket.

3. Reload the unit files:

   ```
   $ sudo systemctl daemon-reload
   ```

4. Restart the docker daemon with new startup options:

   ```
   $ sudo systemctl restart docker.service
   ```

5. Ensure that anyone that has access to the TCP listening socket is a trusted user since access to the docker daemon is root-equivalent.

## MacOS: just install docker client on 

1. brew install docker
2. brew info docker-compose

## mac: 查看端口占用

```shell
lsof -nP -i[tcp|udp][@hostname|hostaddr][:service|port]

lsof -nP -i :80
lsof -nP -i :http

lsof -nP -i tcp:8500

lsof -nP -i tcp@127.0.0.1:8500
```

## mac: 查看端口监听

```shell
lsof -nP -itcp -stcp:listen
```

## mac: 终端tcp/udp流量走shadowsocks代理

```
vim ~/.zshrc  

添加一下3行到文件最后
# proxy list
alias proxy='export all_proxy=socks5://127.0.0.1:1080'
alias unproxy='unset all_proxy
```

验证方法如下：

1. unproxy

   > curl https://ip.cn

2. proxy

   > curl https://ip.cn

3. 对比输出

## mac: unix时间戳

```shell
date +%s
```
## mac: 显示隐藏文件

> ⌘ + ⇧ + . 可以快速显示/隐藏 隐藏文件

```
//显示隐藏文件
defaults write com.apple.finder AppleShowAllFiles -bool true
//不显示隐藏文件
defaults write com.apple.finder AppleShowAllFiles -bool false

// restart finder
```
## mac: 删除所有.DS_Store

```
cd ~; find . -name ".DS_Store"|less
cd ~; find . -name ".DS_Store" -exec rm -f {} \;
```

## mac: 不自动挂载磁盘

```
sudo vifs

UUID=NUMBER none hfs rw,noauto
把NUMBER替换成磁盘的UUID（可在磁盘管理工具中查看）
```



