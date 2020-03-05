# jetson-nano-trick

https://blog.csdn.net/dvd_sun/article/details/88975005  
http://www.manongjc.com/detail/8-ljslmgmshdpltfd.html  

----------------------------------------------------------------------------------------------------------------------------------------

# jetson nano sudo apt-get update ----> 404 not fuund:  
use ustc source which support armhf software.  
update  /etc/apt/sources.list file with content below:  

deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial main multiverse restricted universe  
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-backports main multiverse restricted universe  
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-proposed main multiverse restricted universe  
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-security main multiverse restricted universe  
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-updates main multiverse restricted universe  
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial main multiverse restricted universe  
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-backports main multiverse restricted universe  
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-proposed main multiverse restricted universe  
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-security main multiverse restricted universe  
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-updates main multiverse restricted universe  

but this source maybe cause package install dependence error, download software use:  

deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ xenial main multiverse restricted universe  
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ xenial-security main multiverse restricted universe  
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ xenial-updates main multiverse restricted universe  
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ xenial-backports main multiverse restricted universe  
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ xenial main multiverse restricted universe  
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ xenial-security main multiverse restricted universe  
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ xenial-updates main multiverse restricted universe  
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ xenial-backports main multiverse restricted universe  
deb http://cn.archive.ubuntu.com/ubuntu/ bionic main universe restricted multiverse  
deb http://ports.ubuntu.com/ubuntu-ports/ bionic main universe restricted multiverse  
deb-src http://ports.ubuntu.com/ubuntu-ports/ bionic main universe restricted multiverse #Added by software-properties  
deb http://ports.ubuntu.com/ubuntu-ports/ bionic-security universe restricted main multiverse  
deb-src http://ports.ubuntu.com/ubuntu-ports/ bionic-security universe restricted main multiverse #Added by software-properties  
deb http://ports.ubuntu.com/ubuntu-ports/ bionic-updates universe restricted main multiverse  
deb-src http://ports.ubuntu.com/ubuntu-ports/ bionic-updates universe restricted main multiverse #Added by software-properties  

----------------------------------------------------------------------------------------------------------------------------------------

# 下列软件包有未满足的依赖关系：ros-melodic-desktop-full : 依赖......

software & update choose "server for china",  change the tsinghua source, then after update, can download ROS  
but this will cause sudo apt-get update error  

----------------------------------------------------------------------------------------------------------------------------------------

# sudo rosdep init error:  
ERROR: cannot download default sources list from:  
https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/sources.list.d/20-default.list  
Website may be down.  

(1)  
change to the ustc source, then update.  
sudo -E rosdep init  
(2)  
try mutiple times?  

----------------------------------------------------------------------------------------------------------------------------------------

# rosdep update error:  
reading in sources list data from /etc/ros/rosdep/sources.list.d  
ERROR: unable to process source [https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/osx-homebrew.yaml]:  
	<urlopen error [Errno 111] Connection refused> (https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/osx-homebrew.yaml)  
  
try mutiple times?  

----------------------------------------------------------------------------------------------------------------------------------------

# Jetson Nano利用官方镜像进行安装后，系统已经安装好了JetPack，cuda，cudaa，OpenCV等组件，需要修改下环境变量才可以使用。
sudo gedit ~./bashrc  
文件的最后添加以下三行：  
export PATH=/usr/local/cuda-10.0/bin:$PATH  
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH  
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-10.0  
source ~./bashrc  
输入nvcc -V命令进行测试  
