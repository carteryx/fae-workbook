# 一、环境搭建

  &emsp;&emsp;对于SoC平台，安装好SophonSDK(>=v22.09.02)后内部已经集成了相应的libsophon、sophon-opencv和sophon-ffmpeg运行库包，位于/opt/sophon/下，可直接用于运行环境。我们需要在x86主机上交叉编译程序，使之能够在SoC平台运行。

  &emsp;&emsp;如果例程依赖sophon-sail则需要编译和安装sophon-sail，否则可跳过本章节。我们**需要在x86主机上交叉编译sophon-sail，将在X86平台生成的wheel安装包拷贝至SoC平台上安装**。*提醒：如果是对整个流程不熟悉的人员，一定要分清楚每一步是在X86主机上操作还是在盒子上操作，算力设备只能用于推理！！！*

操作步骤如下：

  &emsp;&emsp;&emsp;&emsp;1. 从算能官网上下载符合环境依赖的sophon-sail的压缩包，执行操作后生成wheel包文件（在X86平台操作）
    
   &emsp;&emsp;&emsp;&emsp; 2. 将wheel包文件拷贝至算力设备，在算力设备上安装sophon-sail（在算力设备上操作）
