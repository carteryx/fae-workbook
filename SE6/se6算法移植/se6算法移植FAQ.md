
**1. 使用scp从控制板直接传输文件，再使用ssh进入算力板操作。在算力板中运行模型报错'ModuleNotFoundError: No module named 'sophon.sail''**

&emsp;&emsp;导致此错误的原因可能是未成功安装sophon.sail或安装了错误版本的sophon.sail，可通过以下方式排查原因：

a. 确认生成wheel包的python版本是否与算力板的python版本一致  (未解决)

b. 确认是否安装opencv-python-headless，运行'pip3 install opencv-python-headless<4.3' (未解决)

c. 配置环境，执行'export PYTHONPATH=$PYTHONPATH:/opt/sophon/sophon-opencv-latest/opencv-python/' (未解决)

d. 在root模式下执行模型运行 (未解决)

e. 在控制板中使用./core_run_command_bynet.sh 脚本进行传输文件和wheel包的安装。(解决)

猜测是由于权限问题导致的错误，未验证
