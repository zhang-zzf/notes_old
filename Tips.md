#### Mac smart quotes and dashes

> 会把2个英文短横变成1个中文长横
>
> 关闭方法：System Preferences -> Keyboard -> Text -> uncheck "Use smart quotes and dashes"



#### enable the remote API for dockerd

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

#### just install docker client on MacOS

1. brew install docker
2. brew info docker-compose.