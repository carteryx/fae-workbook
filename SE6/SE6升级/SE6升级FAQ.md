**1. 升级完后核心板ping不通或ping得通但无法进入核心板系统**
   
  将spi_flash_bm1684.bin文件拷贝至/root/目录下。在控制板上通过串口进入系统不通的核心板：
```
  sudo -i
  source /root/se6_ctrl/se6ctr.sh
  se6ctr_switch_uart 3 (出问题的核心板，如172.16.140.13这里使用3)
  minicom -D /dev/ttyS2
```
  再另打开远程连接窗口进入控制板进行操作：
```
sudo -i

source /root/se6_ctrl/se6ctr.sh

se6ctr_switch_uart 3

se6ctr_set_reset 3
```
回到串口进入的核心板窗口，按jjjjjj键进入BL1 mode，
![image](https://github.com/GLSBZych97/fae-workbook/blob/main/SE6/SE6%E5%8D%87%E7%BA%A7/pics/fig6.png)
看到提示# 后，依次输入以下指令

开启ymodem接收文件： ymodem 0x10100000

依次摁下： Ctrl+A Z S 选择需要传输的spi_flash_bm1684.bin（在箭头指向spi_flash_bm1684.bin文件时需要按空格选中文件再按回车）。

烧录spi flash： spif 0x10100000 0x0 0x120000

烧录完成后： reboot

控制板上执行：reboot_all

等机器启动后进入串口，设备恢复升级状态。

如果遇到了在输入ymodem 0x10100000后一直打印CCCCCCC的问题，可以使用下面的问题2的处理方式解决


**2. 当上述方式无法正常完成烧录，可以通过第二种方法升级**

演示视频：http://219.142.246.77:65000/sharing/QwqZOGAlh(bySE6升级方案说明 - 张泽韬 - Confluence-Sophgo)(注：视频中的ip与现在盒子的算力板ip设置不一致，具体参考本文第一节的ip介绍)

启动时输出NOTICE:  **************时按住回车键，直到进uboot

在算力板的uboot模式下输入以下指令

setenv ramdisk_addr_b 0x310400000

setenv ramdisk_addr_r 0x310000000

setenv chip_type bm1684

setenv scriptaddr 0x300040000


setenv serverip 172.16.140.200 (这个是给1-6号板卡的IP)

setenv ipaddr 172.16.140.11（11~16选一个）

setenv serverip 172.16.150.200  (7-12号板卡的IP)

setenv ipaddr 172.16.150.（11~16选一个）

setenv update_all 0

setenv reset_after 1

i2c dev 1; i2c mw 0x69 1 0

这一步需要确定tftp下载文件是否成功，如果没有成功需要查看ip配置是否错误

tftp ${scriptaddr} /$ota_path/boot_spif.scr

source ${scriptaddr}

在同时对多个算力板升级时，ip地址需要根据算力板变更

