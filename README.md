# jetson-nano-trick

https://blog.csdn.net/dvd_sun/article/details/88975005  
http://www.manongjc.com/detail/8-ljslmgmshdpltfd.html  

----------------------------------------------------------------------------------------------------------------------------------------

# jetson nano sudo apt-get update ----> 404 not fuund:  
(1)  
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

(2)  
dpkg --print-architecture  
dpkg --print-foreign-architectures  
sudo dpkg --remove-architecture ...   

----------------------------------------------------------------------------------------------------------------------------------------

# 下列软件包有未满足的依赖关系：ros-melodic-desktop-full : 依赖......

software & update choose "server for china",  change the tsinghua source, then after update, can download ROS  
but this will cause sudo apt-get update error  

----------------------------------------------------------------------------------------------------------------------------------------

# Jetson Nano利用官方镜像进行安装后，系统已经安装好了JetPack，cuda，cudaa，OpenCV等组件，需要修改下环境变量才可以使用。
sudo gedit ~./bashrc  
文件的最后添加以下三行：  
export PATH=/usr/local/cuda-10.0/bin:$PATH  
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH  
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-10.0  
source ~./bashrc  
输入nvcc -V命令进行测试  

----------------------------------------------------------------------------------------------------------------------------------------

# start jupyter-notebook occur error: UnicodeDecodeError: 'ascii' codec can't decode byte 0xe5 in position 4: ordinal not in range(128)  
sudo gedit ~./bashrc  
文件的最后添加以下：  
export LANG=en_US:UTF-8  
export LANGUAGE=en_US:en  

----------------------------------------------------------------------------------------------------------------------------------------

# install tensorflow-gpu  
https://zhuanlan.zhihu.com/p/98459357  
sudo apt-get install python3-pip  
python3 -m pip install --upgrade pip  
sudo apt install python3-numpy python3-scipy python3-pandas python3-matplotlib python3-sklearn libhdf5-serial-dev hdf5-tools  
sudo pip3 install launchpadlib  
sudo  pip3 install --upgrade setuptools  
sudo pip3 install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v42 tensorflow-gpu==1.14.0+nv19.10   

----------------------------------------------------------------------------------------------------------------------------------------

# pip2 install tensorflow occur error: ERROR: Could not find a version that satisfies the requirement tenserflow==1.12.0 (from versions: none), ERROR: No matching distribution found for tenserflow==1.12.0  
python2 -m pip install --upgrade https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.12.0-py2-none-any.whl  

----------------------------------------------------------------------------------------------------------------------------------------

# 调用TensorFlow时出现FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecate  
sudo pip3 install numpy==1.16.4  

----------------------------------------------------------------------------------------------------------------------------------------

# install ros  
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'  
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654  
sudo apt update  
sudo apt install ros-melodic-desktop-full  
sudo rosdep init  
rosdep update  

----------------------------------------------------------------------------------------------------------------------------------------

# install vscode  
https://packagecloud.io/headmelted/codebuilds/packages/debian/stretch/code-oss_1.32.0-1550644676_arm64.deb/download.deb  
sudo dpkg -i code-oss_1.32.0-1550644676_arm64.deb  

----------------------------------------------------------------------------------------------------------------------------------------

# install gym  
git clone https://github.com/openai/gym.git  
sudo pip3 install -e .  

----------------------------------------------------------------------------------------------------------------------------------------

# 由于没有公钥，无法验证下列签名： NO_PUBKEY 0CC3FD642696BFC8  
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 0CC3FD642696BFC8  
