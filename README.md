# Ubuntu-desktop  

----------------------------------------------------------------------------------------------------------------------------------------

## install cuda10.2+cudnn:  
- https://blog.csdn.net/qq_32408773/article/details/84112166  
- https://blog.csdn.net/u010801439/article/details/80483036  
- https://www.jianshu.com/p/54d30904ed3e  Part2
- https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html

### cuda:  
```
ubuntu-drivers devices  
sudo add-apt-repository ppa:graphics-drivers/ppa  
sudo apt-get update  
sudo apt-get install nvidia-driver-440 nvidia-settings  
sudo reboot  
```
make sure the default graphics card is nvidia gtx
```
wget http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run  
sudo sh cuda_10.2.89_440.33.01_linux.run  
```
to checkout:  
```
cd /usr/local/cuda/samples/1_Utilities/deviceQuery  
sudo make  
sudo ./deviceQuery  
```
### cudnn:  
```
sudo dpkg -i libcudnn7-dev_7.6.5.32-1+cuda10.2_amd64.deb  
sudo dpkg -i libcudnn7_7.6.5.32-1+cuda10.2_amd64.deb  
sudo dpkg -i libcudnn7-doc_7.6.5.32-1+cuda10.2_amd64.deb  
```
to checkout:  
```
sudo cp -r cudnn_samples_v7/ ~  
sudo chmod  -R 777 cudnn_samples_v7/  
cd ~/RL/cudnn_samples_v7/mnistCUDNN  
make  
sudo ./mnistCUDNN  
```
----------------------------------------------------------------------------------------------------------------------------------------

## install tensorflow-gpu:
down .whl file from website:  
-- https://pypi.org/project/tensorflow-gpu/1.14.0/#files  
### python3:  
```
sudo apt-get install python3-pip  
python3 -m pip install --upgrade pip  
sudo apt install python3-numpy python3-scipy python3-pandas python3-matplotlib python3-sklearn libhdf5-serial-dev hdf5-tools  
sudo pip3 install testresources  
sudo pip3 install launchpadlib  
sudo  pip3 install --upgrade setuptools  
sudo pip3 install tensorflow_gpu-1.14.0-cp36-cp36m-manylinux1_x86_64.whl  
```
if import occur: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecate  
```
sudo pip3 install numpy==1.16.4  
```
### python2:  
```
sudo apt-get install python-pip  
python -m pip2 install --upgrade pip  
sudo apt install python-numpy python-scipy python-pandas python-matplotlib python-sklearn libhdf5-serial-dev hdf5-tools  
sudo pip2 install testresources  
sudo pip2 install launchpadlib  
sudo  pip2 install --upgrade setuptools  
sudo pip2 install tensorflow_gpu-1.14.0-cp27-cp27mu-manylinux1_x86_64.whl 
```

----------------------------------------------------------------------------------------------------------------------------------------

# jetson-nano-trick
-  https://blog.csdn.net/dvd_sun/article/details/88975005  
-  http://www.manongjc.com/detail/8-ljslmgmshdpltfd.html  

----------------------------------------------------------------------------------------------------------------------------------------

## change system python version:  
```
sudo gedit ~/.bashrc  
alias python='/usr/bin/pythonx.x'  
source ~/.bashrc
```

----------------------------------------------------------------------------------------------------------------------------------------

## jetson nano sudo apt-get update ----> 404 not fuund:  
```
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
```

----------------------------------------------------------------------------------------------------------------------------------------

## 下列软件包有未满足的依赖关系：ros-melodic-desktop-full : 依赖......
```
software & update choose "server for china",  change the tsinghua source, then after update, can download ROS  
but this will cause sudo apt-get update error  
```

----------------------------------------------------------------------------------------------------------------------------------------

## Jetson Nano利用官方镜像进行安装后，系统已经安装好了JetPack，cuda，cudaa，OpenCV等组件，需要修改下环境变量才可以使用。
```
sudo gedit ~./bashrc  
文件的最后添加以下三行：  
export PATH=/usr/local/cuda-10.0/bin:$PATH  
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH  
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-10.0  
source ~./bashrc  
输入nvcc -V命令进行测试  
```

----------------------------------------------------------------------------------------------------------------------------------------

## start jupyter-notebook occur error: UnicodeDecodeError: 'ascii' codec can't decode byte 0xe5 in position 4: ordinal not in range(128)  
```
sudo gedit ~./bashrc  
文件的最后添加以下：  
export LANG=en_US:UTF-8  
export LANGUAGE=en_US:en  
```

----------------------------------------------------------------------------------------------------------------------------------------

## pip3 install tensorflow-gpu  
```
https://zhuanlan.zhihu.com/p/98459357  
sudo apt-get install python3-pip  
python3 -m pip install --upgrade pip  
sudo apt install python3-numpy python3-scipy python3-pandas python3-matplotlib python3-sklearn libhdf5-serial-dev hdf5-tools  
sudo pip3 install launchpadlib  
sudo  pip3 install --upgrade setuptools  
sudo pip3 install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v42 tensorflow-gpu==1.14.0+nv19.10   
```

----------------------------------------------------------------------------------------------------------------------------------------

## pip2 install tensorflow-gpu  
```
download: https://developer.download.nvidia.cn/compute/redist/jp/v41/tensorflow-gpu/  
sudo pip2 install tensorflow_gpu-1.13.0rc0+nv19.2-cp27-cp27mu-linux_aarch64.whl  
```

----------------------------------------------------------------------------------------------------------------------------------------

## 调用TensorFlow时出现FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecate  
```
sudo pip3 install numpy==1.16.4  
```

----------------------------------------------------------------------------------------------------------------------------------------

## install ros  
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'  
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654  
sudo apt update  
sudo apt install ros-melodic-desktop-full  
sudo rosdep init  
rosdep update  
```

----------------------------------------------------------------------------------------------------------------------------------------

## install vscode  
```
https://packagecloud.io/headmelted/codebuilds/packages/debian/stretch/code-oss_1.32.0-1550644676_arm64.deb/download.deb  
sudo dpkg -i code-oss_1.32.0-1550644676_arm64.deb  
```

----------------------------------------------------------------------------------------------------------------------------------------

## install gym  
```
git clone https://github.com/openai/gym.git  
sudo pip3 install -e .  
```

----------------------------------------------------------------------------------------------------------------------------------------

## 由于没有公钥，无法验证下列签名： NO_PUBKEY 0CC3FD642696BFC8  
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 0CC3FD642696BFC8  
```

----------------------------------------------------------------------------------------------------------------------------------------

## gazebo preparing your world  
```
sudo apt-get install mercurial
hg clone https://bitbucket.org/osrf/gazebo_models models
```

----------------------------------------------------------------------------------------------------------------------------------------

## install pytorch1.4  
```
sudo apt-get install libopenblas-base  
```
python2:  
```
download:https://nvidia.box.com/v/torch-1-4-cp27-jetson-jp43  
sudo pip2 install torch-1.4.0-cp27-cp27mu-linux_aarch64.whl  
```
python3.6:  
```
download:https://nvidia.box.com/v/torch-1-4-cp36-jetson-jp43  
sudo pip3 install Cython  
sudo pip3 install numpy torch-1.4.0-cp36-cp36m-linux_aarch64.whl  
```

----------------------------------------------------------------------------------------------------------------------------------------

## install tianshou  
first install pytorch1.4 in python3  
then,  
```
sudo pip3 install sphinxcontrib-bibtex
sudo pip3 install git+https://github.com/thu-ml/tianshou.git@master
```

----------------------------------------------------------------------------------------------------------------------------------------

## python2 launch tensorboard err: cannot import _massage  
```
PATH: pip3 show tensorboard  
sudo gedit ~/.bashrc
alias tensorboard='python3 PATH/tensorboard/main.py'  
source ~/.bashrc
```

----------------------------------------------------------------------------------------------------------------------------------------
