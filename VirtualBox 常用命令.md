### VirtualBox 常用命令

1. Headless start

   > VBoxManage startvm <uuid|vmname> [--type gui|headless|separate]

2. Pause/Resume

   > VBoxManage controlvm <uuid|vmname> pause|resume|poweroff|savestate|reset

3. 查看vm信息

   > VBoxManage showvminfo <uuid|vmname> [--details]

4. 控制Guest

   > TODO VBoxManage guestcontrol 