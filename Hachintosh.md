## 黑苹果

> TODO
>
> 更换硬件后windows压测
>
> 验证HEVC硬件加速
>
> Imac18.3 尝试

### Hardware

>Intel Ethernet Connection I219-V/Intel I211 Gigabit Network Connection

### Useful tips

format u disk

> diskutil partitionDisk /dev/disk1 1 GPT HFS+J "install_osx" R

how to install/uninstall kexts

>sudo cp -R KextToInstall.kext /Library/Extensions
>
>sudo kextcache -i /
>
>sudo rm -Rf /Library/Extensions/KextToInstall.kext

how to add/remove BIOS start options

>bcfg boot dump
>
>bcfg boot rm 1
>
>bcfg boot mv 2 0
>
>bcfg boot add 3 fs0:\\EFI\boot/bootx64.efi "Clover"
>
>[more](https://wiki.archlinux.org/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell)
>
>search keys: uefi shell

###MacOS 10.14.3

1. target

   > native CPU

   > DiskPlay 4K@60 DP/HDMI2.0/HDMI

   >shutdown/restart/sleep/wakeup

   >navtive WI-FI/BT

   >iCloud/iMessage/Handoff/共享剪贴板/Watch unlock/电话

   >声音自动切换/麦克风测试/apfs日志

   >native USB/3.0 5G

   >Ethernet cards just need one to work

2. 遇到问题及解决方案

   1. 睡眠后U盘未被正常弹出

      > BIOS XMP 导致，关闭XMP，内存手动超频2666Mhz

   2. USB 端口太多

      | location            | ports     |
      | ------------------- | --------- |
      | front left          | HS01/SS01 |
      | front right         | HS02/SS02 |
      | BT                  | HS10      |
      | back up left        | HS03/SS03 |
      | back up right       | HS04/SS04 |
      | back down right     | HS06/SS06 |
      | back down rightleft | HS05/SS05 |
      | back down leftright | HS08/SS08 |
      | back down left      | HS07/SS07 |
      | USB-C               | HS09/SS09 |

      共19个端口，去掉back down 4个USB3.0和USB-C的2.0

      19 个 - 5 个（底部4个USB3.0 + type-c 2.0)，剩下14个端口

      1. Install USBInjectAll.kext in /Library/Extensions
      2. 修改SSDT-UIAC.dsl后编译成SSDT-UIAC.aml，放到Clover的/ACPI/patched中

   3. 