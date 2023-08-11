# Linux基础
## Linux发行版

Linux 是一个开源的操作系统内核，但由于其开放性和灵活性，产生了许多不同的 Linux 发行版（Distribution，缩写为 "distro"）。每个发行版都基于 Linux 内核，并包含了一系列的工具、库、桌面环境和应用程序，以创建一个完整的操作系统。

## 以下是一些常见的 Linux 发行版：

1.Ubuntu： 基于 Debian，被广泛用于桌面和服务器。它有不同的版本，如 Ubuntu Desktop、Ubuntu Server 等，以满足不同用途的需求。

2.Debian： 一个稳定、强大的发行版，被用于服务器和工作站。它也是许多其他发行版的基础。

3.Fedora： 由社区支持的发行版，强调最新的软件和技术。Fedora 也是 Red Hat Enterprise Linux（RHEL）的上游项目。

4.CentOS： 基于 RHEL 的重建版本，致力于提供一个免费的企业级操作系统。

5.openSUSE： 提供稳定和强大的桌面和服务器发行版，有两个主要版本：openSUSE Leap 和 openSUSE Tumbleweed（滚动发布）。

6.Arch Linux： 面向高级用户的发行版，强调简单性、定制性和文档。

7.Manjaro： 基于 Arch Linux，旨在为普通用户提供友好的体验，并提供了预配置的桌面环境。

8.Linux Mint： 基于 Ubuntu 或 Debian，专注于提供易于使用的桌面环境。

9.Elementary OS： 基于 Ubuntu，以精美的界面和用户友好的设计著称。

10.Kali Linux： 专为网络安全和渗透测试而设计的发行版，内置了各种安全工具。
## Linux文件结构

1./：根目录

2./bin:系统指令

3./usr:应用程序

4./var:可变文件，日志数据库等

5./dev:外设

6./lib:库

7./proc:系统运行时文件

8./etc:系统配置文件

9./home:用户文件

10.temp:临时文件

11.opt:安装文件

12./mnt:挂载文件
## Linux命令行
Linux 命令行是在终端（Terminal）或命令行界面中输入和执行命令的方式，用于与 Linux 操作系统进行交互和管理。命令行是一个强大的工具，可以用于执行各种系统任务、文件操作、软件安装、配置管理等。
## 基本操作指令
以下是一些常见的 Linux 命令行命令及其用法：

1.pwd： 显示当前工作目录的完整路径。
```
pwd
```
2.ls： 列出当前目录中的文件和子目录。
```
ls
ls -l  # 以长格式显示文件信息
ls -a  # 显示所有文件，包括隐藏文件
```
3.cd： 切换工作目录。
```
cd /path/to/directory  # 切换到指定目录
cd ..  # 切换到上级目录
```
4.mkdir： 创建新目录。
```
mkdir new_directory
```
5.rm： 删除文件或目录。
```
rm file.txt  # 删除文件
rm -r directory  # 递归删除目录及其内容
```
6.cp： 复制文件或目录。
```
cp file.txt new_location/  # 复制文件到指定目录
cp -r directory new_location/  # 递归复制目录及其内容
```
7.mv： 移动文件或重命名文件。
```
mv file.txt new_location/  # 移动文件到指定目录
mv old_name.txt new_name.txt  # 重命名文件
```
8.touch： 创建空文件或更新文件的访问时间。
```
touch file.txt
```
9.cat： 显示文件内容。
```
cat file.txt
```
10.echo： 在终端显示文本。
```
echo "Hello, world!"
```
11.grep： 在文件中搜索特定文本。
```
grep "search_text" file.txt
```
12.chmod： 修改文件或目录的权限。
```
chmod permissions file.txt
```
>r读取权限，数字4
>w写入权限，数字2
>x执行权限，数字1
>-不具备权限 数字0

13.chown： 修改文件或目录的所有者。
```
chown new_owner file.txt
```
14.ps： 显示运行的进程列表。
```
ps aux
```
15.kill： 终止运行中的进程。
```
kill process_id
```
16.apt-get 或 yum： 在 Debian/Ubuntu 或 CentOS/RHEL 等系统上安装和管理软件包。
```
sudo apt-get install package_name
sudo yum install package_name
```
17.df： 显示文件系统磁盘空间使用情况。
```
df -h
```
18.top 或 htop： 显示系统资源使用情况和运行中的进程。
```
top
htop
```
这只是一些常见的 Linux 命令行命令。Linux 命令行界面提供了丰富的功能和工具，可以满足各种系统管理和操作需求。可以通过命令行界面执行任务，也可以编写脚本自动化一系列操作

## VIM编辑器
`vim`（Vi IMproved）是一款强大的文本编辑器，是 Unix-like 系统中常用的编辑工具之一。它是 vi（Visual Editor）编辑器的改进版本，提供了许多增强功能和功能，适用于编辑各种文本文件，包括代码、配置文件等。
以下是一些常见的 vim 编辑器的基本用法：

1.打开文件： 在终端中输入以下命令来打开一个文件：
```
vim filename
```
2.编辑模式： 打开文件后，默认处于命令模式（Command mode）。按下 `i` 进入插入模式（Insert mode），此时可以输入文本。
3.插入文本： 在插入模式下，键入所需的文本。按 `Esc` 键返回命令模式。
4.保存文件： 在命令模式下，输入 ：`w` 并按回车键保存文件。
5.保存并退出： 在命令模式下，输入 ：`wq` 并按回车键保存文件并退出 `vim`。
6.退出而不保存： 在命令模式下，输入 :`q!` 并按回车键，强制退出 `vim` 而不保存修改。
7.导航和移动光标： 在命令模式下使用以下键来移动光标：
* `h`：向左移动
* `j`：向下移动
* `k`：向上移动
* `l`：向右移动

8.删除文本： 在命令模式下使用以下命令来删除文本：
* `x`：删除光标所在位置的字符
* `dd`：删除光标所在行

9.复制和粘贴： 在命令模式下使用以下命令来复制和粘贴文本：
* `yy`：复制光标所在行
* `p`：粘贴复制的文本

10.搜索和替换： 在命令模式下使用以下命令来搜索和替换文本：
* `/search_term`：搜索指定的文本
* `:s/search_term/replace_term/g`：在整个文件中替换文本

11.撤销和重做： 在命令模式下使用以下命令来撤销和重做操作：
* `u`：撤销上一步操作
* `Ctrl + r`：重做上一步撤销的操作

12.分屏显示： 在命令模式下使用以下命令来分屏显示文本：
* `:split`：水平分屏
* `:vsplit`：垂直分屏

13.多文件编辑： 在命令模式下使用以下命令来编辑多个文件：
* `:e filename`：打开另一个文件
* `:n`：跳转到下一个文件
* `:prev` 或 `:N`：跳转到上一个文件

14.显示行号： 在命令模式下使用以下命令来显示行号：
* `:set number`

这只是一些 vim 编辑器的基本用法。vim 有非常丰富的功能和命令，可以用于高效编辑文本文件。用户可以通过 vim 的内置帮助系统（在命令模式下输入 :help 并按回车键）了解更多详细信息和高级用法。
## Linux包管理工具
1.dpkg
* `dpkg -i`:安装本地deb包
* `dpkg  -L`：显示软件包文件的位置，配置文件在/etc

2.apt:apt的线上软件源配置文件位于/etc/apt/sources.list
* `apt install`:从源中安装包，会自动解决依赖问题
* `apt upgrade`:升级所有可升级的包
## Linux网络工具
1.ifconfig:net-tools包的工具，常用来获取网卡状态

2.ping、telnet、netplan

* `ping<ip>`:可以测试网络联通
* `telnet<ip><port>`:测试端口
* `vim /etc/netplan/**.yaml`:修改对应网卡ip,netplan apply应用更改
## Linux远程工具
1.ssh远程格式：ssh <username>@<host>连接，回车后输入密码

2.scp远程复制格式：<file> <username>@<host>:/path/,回车输入密码  -r文件夹

