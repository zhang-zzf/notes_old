## Local_VMS

VM_local

ssh-add ~/.ssh/local_vms/id_rsa

#### vm1安装的软件

- JDK1.8

- Mysql
  - systemctl start/stop mysqld
  - root/db_Dba_root0.

- Docker
- filebeat

####vm2安装的软件

- filebeat

#### consul

vm1:

```
nohup /usr/local/consul/consul agent -node=vm1 -ui -server -bootstrap -client=0.0.0.0 -bind=192.168.56.1 -data-dir=/var/lib/consul -enable-script-checks=true -config-dir=/etc/consul.d &>/var/log/consul/consul.log &
```

vm2:

```
nohup /usr/local/consul/consul agent -node=vm2 -ui -client=0.0.0.0 -bind=192.168.56.2 -data-dir=/var/lib/consul -join 192.168.56.1 &>/var/log/consul/consul.log &
```

### CentOS 配置

1. 配置IP

   ```
   vi /etc/sysconfig/network-scripts/ifcfg-enp0s3
   
   IPADDR=192.168.56.x
   PREFIX=24
   ```

2. 设置hostname

   ```
   hostnamectl set-hostname vmx
   ```

3. 重启网卡

   ```
   ifdown enp0s10;ifup enp0s10
   ```

   