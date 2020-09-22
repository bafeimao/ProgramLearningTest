[toc]

# VMvare虚拟机配置

## centos 7最小化安装后配置静态ip

```shell
1所有操作均为root管理员用户

ip addr	#查看本机ip地址和网卡名称
vi /etc/sysconfig/network-scripts/ifcfg-查看的本机网卡名称 #配置静态ip
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.111.101
GATEWAY=192.168.111.2 #网关查看vmware虚拟网络编辑器NAT模式的网关
NETMASK=255.255.255.0
DNS1=8.8.8.8
DNS2=144.144.144.144

Systemctl restart network.service	#重启网络服务
ping 外网内网主机间的连通性   需要关闭主机的防火墙
克隆两台虚拟机名称为slave1  slave2，本机为master
```

## 配置主机名称hostname

```shell
此处举一种方法
vi /etc/hostname
dd命令删掉内容  i插入  输入master  :wq!保存退出
另两台虚机分别为slave1，slave2
重启后生效
```

## 设置hosts

```shell
三台虚机都操作
vi /etc/hosts
192.168.111.101 master
192.168.111.102 slave1
192.168.111.103 slave2
```

## 关闭selinux和防火墙

```shell
三台虚机都操作
vi /etc/selinux/config
SELINUX=disable
source /etc/selinux/config

systemctl stop firewalld.service	#关闭防火墙
systemctl status firewalld.service	#查看防火墙状态
systemctl disable firewalld.service #禁止防火墙服务器，防止重启防火墙自动开启
```

## 设置ssh免密登陆

```shell
三台虚机都要
设置前可先将.ssh文件夹删除
cd ~/.ssh
ssh-keygen -t rsa	#一直回车直到出现密钥
ssh-copy-id root@master	#拷贝公钥到所有机器
ssh-copy-id root@slave1
ssh-copy-id root@slave2

ssh master	#测试免迷登陆
ssh slave1
ssh slave2

```

# JDK安装和HA安装

```shell
mkdir -p /opt/module	#指定目录创建文件夹
mkdir -p /opt/software
xftp上传需要用到的包到software
scp -r /opt/software/ root@slave1:/opt/software
scp -r /opt/software/ root@slave2:/opt/software

rpm -qa |grep java  #查询是否安装JDK
rpm -r 软件包   #卸载
which java  #查看JDK安装路径
tar -zxvf jdk-8u171-linux-x64.tar.gz -C /opt/module/ #解压到指定文件夹
cd /opt/module
mv jdk1.8.0_171/ jdk1.8
vi ~/.bash_profile #配置环境变量
#JAVA_HOME
export JAVA_HOME=/opt/module/jdk1.8
export PATH=$PATH:$JAVA_HOME/bin

#HADOOP_HOME
export HADOOP_HOME=/opt/module/hadoop-2.6.0
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin

source ~/.bash_profile
java -version

hadoop version


```
