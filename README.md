# jetson-nano-trick

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
