# 一、环境搭建

  &emsp;&emsp;对于SoC平台，安装好SophonSDK(>=v22.09.02)后内部已经集成了相应的libsophon、sophon-opencv和sophon-ffmpeg运行库包，位于/opt/sophon/下，可直接用于运行环境。我们需要在x86主机上交叉编译程序，使之能够在SoC平台运行。

  &emsp;&emsp;如果例程依赖sophon-sail则需要编译和安装sophon-sail，否则可跳过本章节。我们**需要在x86主机上交叉编译sophon-sail，将在X86平台生成的wheel安装包拷贝至SoC平台上安装**。*提醒：如果是对整个流程不熟悉的人员，一定要分清楚每一步是在X86主机上操作还是在盒子上操作，算力设备只能用于推理！！！*

操作步骤如下：

  &emsp;&emsp;&emsp;&emsp;1. 从算能官网上下载符合环境依赖的sophon-sail的压缩包，执行操作后生成wheel包文件（在X86平台操作）
    
   &emsp;&emsp;&emsp;&emsp; 2. 将wheel包文件拷贝至算力设备，在算力设备上安装sophon-sail（在算力设备上操作）

**注意**：（在开始安装之前，首先要确认开发环境（即X86主机）的python版本是否与算力设备的python版本一致，如果不一致请在开发环境下安装相同版本的python后再执行操作）


1. 从官网获取与算力板版本一致的SDK，本文所使用的为SE6 V22.12.01刷机包，对应的SDK版本为V22.12.01。进入算能官网>>服务与支持>>技术资料>>开发资料找到对应版本的SDK进行下载（technical center (sophgo.com)），将SDK拷贝至开发环境中并进行解压。

2. 确认编译过程中需要用到相关文件的目录，如果遇到路径不存在请自行进行解压相关文件，本文中记录的都是以Release_221201-public为根目录的相对路径，所有操作都在Release_221201-public/目录下。

```
# 确认python3的lib路径和python3的可执行文件路径
whereis python3
 
 
# 安装gcc-aarch64-linux-gnu工具链
sudo apt-get install gcc-aarch64-linux-gnu g++-aarch64-linux-gnu
 
# 在Release_221201-public/sophon-sail_20221227_085400/sophon-sail/路径下创建build文件夹并且进入文件夹中
cd Release_221201-public/sophon-sail_20221227_085400/sophon-sail
mkdir build && cd build
 
 
# 执行编译命令 （以下选其一，根据自己的目录修改参数，根据是否需要编译出包含bmcv,sophon-ffmpeg,sophon-opencv）
cmake -DBUILD_TYPE=soc  \
 -DCMAKE_TOOLCHAIN_FILE=/data/changhui/changhui_data/Release_221201-public/sophon-sail_20221227_085400/sophon-sail/cmake/BM168x_SOC/ToolChain_aarch64_linux.cmake \
 -DPYTHON_EXECUTABLE=/usr/bin/python3.8 \
 -DCUSTOM_PY_LIBDIR=/usr/lib \
 -DLIBSOPHON_BASIC_PATH=/data/changhui/changhui_data/Release_221201-public/libsophon_20221227_025400/libsophon_0.4.4_aarch64/opt/sophon/libsophon-0.4.4 \
 -DFFMPEG_BASIC_PATH=/data/changhui/changhui_data/Release_221201-public/sophon-mw_20221227_040823/sophon-mw_0.5.1_aarch64/opt/sophon/sophon-ffmpeg_0.5.1 \
 -DOPENCV_BASIC_PATH=/data/changhui/changhui_data/Release_221201-public/sophon-mw_20221227_040823/sophon-mw_0.5.1_aarch64/opt/sophon/sophon-opencv_0.5.1 ..
make sail
 
 
# 打包生成python wheel,生成的wheel包的路径为‘python/soc/dist’,文件名为‘sophon_arm-3.3.0-py3-none-any.whl’
cd ../python/soc
chmod +x sophon_soc_whl.sh
./sophon_soc_whl.sh
 
# 将‘sophon_arm-3.3.0-py3-none-any.whl’拷贝到SE6控制板的linaro目录下
# 连接SE6设备控制板进入root账户，将sophon_arm-3.3.0-py3-none-any.whl'文件下发至各算力板
sudo -i
./core_run_command_bynet.sh "~/script/scp_file2dir_local.exp 192.168.150.1 linaro linaro ~/sophon_arm-3.3.0-py3-none-any.whl ~/" linaro linaro
 
# 在各算力版上安装sail
./core_run_command_bynet.sh "pip3 install sophon_arm-3.3.0-py3-none-any.whl --force-reinstall" linaro linaro
 install sail on all of the computing modules
 
# 进入算力设备确认sophon-sail是否安装成功，为报错即安装成功
ssh linaro@172.16.140.11
python3
>>>import sophon
```


