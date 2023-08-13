## Docker简介
Docker是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可抑制的容器中，然后发布到任何流行的Linux机器上，也可以实现虚拟化。容器完全使用沙盒机制，相互之间不会存在任何接口。几乎没有性能开销，可以很容易的在机器和数据中心运行。最重要的是，他们不依赖于任何语言、框架或者包装系统。

## 以下是一些常见的 Docker 命令及其用法

### 1.info|version
```
docker info       #显示docker的系统信息，包括镜像和容器的数量
```
```
docker version    #显示docker的版本信息
```

### 2.帮助命令
```
docker 命令 --help      #帮助命令
```
### 3.镜像管理
```
docker images   #查看所有本地主机上的镜像 
```
```
docker search   #搜索镜像
```
```
docker pull     #下载镜像 
```
```
docker rmi      #删除镜像 
```
### 4.容器命令
```
docker run -it -p 5900:5900 siomiz/chrome    #run一个容器，-it交互式，-p src:des端口映射
```
```
docker ps –a   #查看所有docker（包括已停止的）
```
```
docker rm 容器id    #删除指定容器
```
### 5.删除所有容器
```
docker rm -f $(docker ps -aq)  	 #删除所有的容器
```
```
docker ps -a -q|xargs docker rm  #删除所有的容器
```
### 6.启动和停止容器
```
docker start 容器id	#启动容器
```
```
docker restart 容器id	#重启容器
```
```
systemctl enable docker  #docker开机自启动
```
```
docker stop 容器id	#停止当前正在运行的容器
```
```
docker kill 容器id	#强制停止当前容器
```
## 7.退出容器
```
exit 		#容器直接退出
```
```
ctrl+p+q    #run进去容器，ctrl+p+q退出，容器不停止
```
### 8.其他常用命令
```
docker run -d 镜像名  #后台启动命令
```
```
docker logs 	#查看日志
```
```
docker login    #登录库，推送镜像
```
```
docker top 容器id 	#查看容器中进程信息ps
```
```
docker inspect <dockerID>   #查看某个容器所有信息
```
```
docker exec 	#进入当前容器后开启一个新的终端，可以在里面操作。
```
```
docker attach 		# 进入容器正在执行的终端
```
```
docker cp 容器id:容器内路径  主机目的路径	  #从容器内拷贝到主机上
```










