
# 一、SE6简单介绍
## 1. 网络拓扑：
### 1.1 网络拓扑介绍
> SE6 由一个控制板和两个算力板组成，每个算力板由6个算力核心板组成。一共 12个算力核心板和一个控制板。控制板有3 个网口: **enp3s0**(即 WAN)，**eth0**(即 LAN1)，**eth1**(即LAN2)。默认情况 enp3s0 为 DHCP 方式（盒子每次重启或刷机均会提供一个新的ip，需要使用ifconfig进行查看）

算力板0的6块核心板 为 172.16.140.11~172.16.140.16

算力板1的6块核心板 为 172.16.150.11~172,16.150.16

核心板的 ip 是由控制板在开机前设置给核心板，如果单独修改控制板 eth0 或者 eth1 的可能会导致核心板无法连通的问题
![image](https://github.com/GLSBZych97/fae-workbook/blob/main/SE6/SE6%E5%8D%87%E7%BA%A7/pics/fig1.png)



SE6 控制板默认会为所有的算力核心板映射 12个端口 (22 端口)。端口号为算力板0: 10021-10026 ; 算力板1: 20021-20026

### 1.2 网络拓扑相关操作
1.2.1 WAN IP获取：

使用micro usb数据线连接串口和PC，使用串口登录设备后使用ifconfig命令查看WAN(enp3s0)口IP。
![image](https://github.com/GLSBZych97/fae-workbook/blob/main/SE6/SE6%E5%8D%87%E7%BA%A7/pics/fig2.png)

1.2.2 WAN IP修改

WAN IP可以设置为DHCP（每次开机控制板自动分配IP）或者是固定IP（根据下面的1.2.2.1来设置），默认为DHCP模式。

1.2.2.1 使用bm_set_ip的命令修改IP为固定IP：
```
# bm_set_ip 网口 IP netmask dns
bm_set_ip enp3s0 192.168.1.107 255.255.255.0 192.168.1.1 192.168.1.1
```
1.2.2.2 使用bm_set_ip_auto命令修改IP为DHCP

控制板 WAN 口 (enp3s0) 修改ip 时，不会做自动做端口映射，需用户手动执行/root/se6 ctrl/iptable_setup.sh，配置端口映射。

核心板的 ip 是由控制板在开机前设置给核心板，如果单独修改控制板 eth0 或者 eth1 的ip，可能会导致核心板无法连通的问题和端口映射的问题。一般不建议修改核心板的IP，如果修改需要执行使用reboot_all 命令重启整机。

# 二、SE6升级
SE6升级分为控制**板升级** 和**核心板**升级。

## 1. 控制板升级
### 1.1 SD卡刷升级

 推荐使用MicroSD卡对SE6控制板进行系统升级，目前SE6升级包有以下两个版本：
 
算能官网>>服务与支持>>技术资料>>开发资料>>V2.7.0>>SE6 sdcard 2.7.0(technical center (sophgo.com))

算能官网>>服务与支持>>技术资料>>开发资料>>Others>>SE6(technical center (sophgo.com))（最新版）

SD卡刷升级步骤：

1. 准备一张容量不低于16GB的MicroSD卡.

2. 对该MicroSD卡进行格式化操作，确保一个分区，例如“/dev/sdal”。

3. 拷贝需要升级版本的所有文件到MicroSD卡根目录.

4. 确保SE6处于下电状态，插入MicroSD卡，并将设备上电，此时STAT灯呈现为红色（常亮）状态。

5. 等待设备升级完成，待STAT灯由红色（常亮）变为绿色（闪烁）状态后，将设备下电，并将MicroSD卡移除。

6. 升级完成，将SE6重新上电

### 1.2无需SD卡升级方法（参考xinming.zhanghttps://wiki.sophgo.com/x/x0clAw）

a、登录SE6算力服务器后，先执行如下命令，确认当前SE6算力服务器版本信息
```
linaro@bm1684:~$ sudo su

root@bm1684:/home/linaro# cd /root/se6_ctrl/script/

root@bm1684:~/se6_ctrl/script# bm_version

BUILD TIME: 20220531_022200

VERSION: 2.7.0

KernelVersion : Linux bm1684 4.9.38-bm1684-v10.6.0-00575-ga2df70e #1 SMP Tue May 31 15:37:40 CST 2022 aarch64 aarch64 aarch64 GNU/Linux

HWVersion: 0x01

MCUVersion: 0x16
```
b、执行如下命令，将SE6算力服务器侧/root/ota目录清空
```
root@BH0007-host:/home/linaro# cd /data/ota/

root@BH0007-host:/data/ota# rm -r *

root@BH0007-host:/data/ota# ls -l

total 0

root@BH0007-host:/data/ota#
```
c、通过xftp或winscp工具，将提前获取到的se6_ctl_sdcard文件夹下的升级包拷贝到SE6算力服务器的/data/ota目录下，如下图
![image](https://github.com/GLSBZych97/fae-workbook/blob/main/SE6/SE6%E5%8D%87%E7%BA%A7/pics/fig3.png)
![image](https://github.com/GLSBZych97/fae-workbook/blob/main/SE6/SE6%E5%8D%87%E7%BA%A7/pics/fig4.png)


d、执行如下命令，启动SE6算力服务器控制板版本升级

root@BH0007-host:/home/linaro# sudo -i

root@BH0007-host:~# cd /data/ota/

root@BH0007-host:/data/ota# chmod +x local_update.sh

root@BH0007-host:/data/ota# ./local_update.sh md5.txt

注：控制板升级大约耗时5min左右
![image](https://github.com/GLSBZych97/fae-workbook/blob/main/SE6/SE6%E5%8D%87%E7%BA%A7/pics/fig5.png)


## 2. 核心板升级

**SE6的算力板无法直接通过3.0.0版本之前（包括3.0.0版本）升级到3.0.0版本之后的版本。如果强行升级会导致严重后果（算力板一直自动重启，不能进入系统！！！如果不小心强行升级了可以通过问题1和问题2的方式解决。）可以通过在算力板上运行bm_version命令查看当前SDK版本：如果显示KernelVersion版本5.4则为3.0.0版本之后的版本，如果是4.9则为3.0.0版本之前（包括3.0.0版本）的版本**


### 2.1 核心板升级步骤
核心板升级需要注意升级前的版本为多少，现在有两种情况：4.9>>5.4 和 5.4>>5,4

**2.1.1 核心板4.9升级为5.4操作步骤**

1. 拷贝spi_flash.bin 从控制板升级包（sdcard包）到控制版/home/linaro 目录
2. sudo -i
3. 升级spi_flash.bin
   1. . cd /root/se6_ctrl/script/
   2.  ./core_run_command_bynet.sh "~/script/scp_file2dir_local.exp 192.168.2.104（控制板 wan口ip） linaro linaro ~/spi_flash.bin ~ /" linaro linaro
   3. cp /usr/sbin/flash_update /home/linaro/
   4. /core_run_command_bynet.sh "~/script/scp_file2dir_local.exp 192.168.2.104（控制板wan 口ip） linaro linaro ~/flash_update ~ /" linaro linaro
   5. ./core_run_command_bynet.sh "sudo ./flash_update -i spi_flash.bin -b 0x6000000" linaro linaro
5. ./core_run_command_bynet.sh "~/tftp_update/mk_bootscr.sh" linaro linaro
6. source ~/se6_ctrl/se6ctr.sh ;se6ctr_set_reset 1

整个升级大概15分钟，可以使用 ./core_run_command_bynet.sh "bm_version" linaro linaro 检查版本 (由于目前有cpld的bug，只能等待15分钟左右手动上下电，再检查版本 )

**2.1.2 核心板5.4升级为5.4操作步骤**

1. sudo -i
2. cd /root/se6_ctrl/script/
3. ./core_run_command_bynet.sh "~/tftp_update/mk_bootscr.sh" linaro linaro
4. ./core_run_command_bynet.sh "sudo reboot" linaro linaro
   
整个升级大概15分钟，可以使用 ./core_run_command_bynet.sh "bm_version" linaro linaro check版本
**2.1.3 升级单个核心板**

参考第一节中各核心板的编号和ip，最后的数字5即为第五块核心板172.16.140.15。

1. sudo -i
2. cd ~/se6_ctrl/script/
3. ./core_run_command_bynet.sh "~/tftp_update/mk_bootscr.sh" linaro linaro 5
4. ./core_run_command_bynet.sh "sudo reboot" linaro linaro 5
