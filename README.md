anacode, nvdia, pytorch, 创建虚拟内存 

大家参加比赛的时候经常会被高配置人民币玩家拒之门外，或者图像类比赛到了第二轮就由于机器配置不行打不了。

下面是教学如何配置anacode, nvdia, pytorch, 创建虚拟内存 教学。

如果你们有学校的服务器，那么也会经常遇到下面的配置问题，可以按照下面步骤配置好；
如果你没服务器，建议大家可以去申请一下google cloud 服务器，300美金的免费使用，完全够打一个比赛，建议你每跑一次，就把主机示例删掉，第二天再重新安装环境，不然挂在那里免费的钱很快就没了（等你用完了一个，再申请一个新的账号，循环搞起来）。


基本步骤

1) sudo apt install bzip2 tmux zsh htop git-core 
2) export PATH=/root/anaconda3/bin:$PATH

anaconda 

1) wget https://repo.anaconda.com/archive/Anaconda3-5.2.0-Linux-x86_64.sh
2) bash Anaconda3-5.2.0-Linux-x86_64.sh

nvdia

wget http://us.download.nvidia.com/tesla/384.66/nvidia-diag-driver-local-repo-ubuntu1404-384.66_1.0-1_amd64.deb
1) sudo apt-key add /var/nvidia-diag-driver-local-repo-384.66/7fa2af80.pub
2) sudo dpkg -i nvidia-diag-driver-local-repo-ubuntu1404-384.66_1.0-1_amd64.deb
3) sudo apt-get update`
4) sudo apt-get install cuda-drivers

cuda 

#https://developer.nvidia.com/cuda-80-ga2-download-archive

1) wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
2) sudo dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
3) sudo apt-get update
4) sudo apt-get install cuda

pytorch

#https://pytorch.org/

1)bash
2)conda install pytorch torchvision -c pytorch
3)conda install pytorch-cpu torchvision-cpu -c pytorch # no cuda，安装了2，那就不用管3了。


创建虚拟内存

#停止所有的swap分区

swapoff -a 

#创建要作为swap分区的文件:增加1GB大小的交换分区，则命令写法如下，

#其中的count等于想要的块的数量（bs*count=文件大小）

dd if=/dev/zero of=/root/swapfile bs=1M count=153600

#格式化为交换分区文件:

mkswap /root/swapfile #建立swap的文件系统

#启用交换分区文件:

swapon /root/swapfile #启用swap文件

#(非必做)使系统开机时自启用，在文件/etc/fstab中添加一行：

/root/swapfile swap swap defaults 0 0


示例：创建150M 虚拟内存

sudo su
dd if=/dev/zero of=/root/swapfile bs=1M count=153600
mkswap /root/swapfile 
swapon /root/swapfile


如果配置过程中有什么疑惑可以在issues 直接给我留言

