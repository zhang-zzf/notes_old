####CentOS 搭建Shadowsocks服务端

1. 安装

   ```shell
   yum install python-setuptools;easy_install pip;pip install shadowsocks
   ```

2.  配置

   新建/etc/shadowsocks.json文件，内容如下

   ```json
   {
       "server": "0.0.0.0",
       "local_address": "127.0.0.1",
       "local_port": 1080,
       "port_password": {
           "8389": "Zfeng03295813",
           "8489": "L.xu20180816",
           "8589": "G.tao20180830",
           "8689": "W.weilong20190305"
       },
       "timeout": 300,
       "method": "aes-256-cfb",
       "fast_open": false
   }	 
   ```

3. 运行

   1. 前台运行(Ctrl+C或者关闭终端服务会自动停止)：

      ```shell
      ssserver -c /etc/shadowsocks.json
      ```

   2. 后台运行(推荐，关闭终端后服务会继续运行)：

      ```shell
      ssserver -c /etc/shadowsocks.json -d start
      
      ssserver -c /etc/shadowsocks.json -d stop
      
      ssserver -c /etc/shadowsocks.json -d stop;ssserver -c /etc/shadowsocks.json -d start
      ```

4. 加速运行，youtube 1080P 无压力

   ```shell
   nohup java -Xmx128M -XX:+UseG1GC -XX:MaxGCPauseMillis=8 -jar /fs/fs.jar &> /fs/server.log  &
   ```

5. 