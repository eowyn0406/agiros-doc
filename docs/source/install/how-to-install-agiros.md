<link rel="stylesheet" type="text/css" href="/root/work/scrapy-cookbook/source/auto-number-title.css" />

# AGIROS-LOONG 安装及使用指南

本指南用于指导用户从零开始使用Agiros-Loong机器人操作系统。

## 基础操作系统安装（openEuler 22.03 LTS SP2）

### 虚拟机/实体机安装openEuler22.03LTS SP2版本。

参考虚拟机安装openEuler 22.03 + ROS2教程 及 实体机安装OE22.03及ROS 教程。安装UKUI界面，做好虚拟机环境备份。

## 安装AGIROS-LOONG

### 禁用其他软件源（干净系统跳过此步骤）

```bash
cd /etc/yum.repos.d
# 若之前安装过欧拉系统的ROS软件，需要先移除ROS源
mv openEulerROS.repo openEulerROS.repo.bak
```

### 添加AGIROS软件源文件

```bash
 wget -O /etc/yum.repos.d/agiros.repo http://1.94.193.239/yumrepo/openeuler2203sp2/openeuler2203sp2.repo
 ```
 
此时本地/etc/yum.repo.d/目录下会生成一个agiros.repo文件，repo文件内容如下：

```bash
#软件源名称，将被yum取得并识别
[agiros-loong] 
#软件仓库的名称
name=agiros-loong 
#这一行的意思是指定一个baseurl（源的服务器地址）
baseurl=http://1.94.193.239/yumrepo/openeuler2203sp2/agiros 
#这个选项表示这个repo中定义的源是启用的，0为禁用
enabled=1 
#这个选项表示这个repo中下载的rpm将进行gpg的校验，已确定rpm包的来源是有效和安全的
gpgcheck=0 
```
### 在软件源添加完成后，更新软件包列表

```bash
yum clean all
yum makecache
```

### 安装Agiros-loong-0.1.0

```bash
# 安装agiros-loong
yum install agiros-loong-agiros-base agiros-loong-turtlesim
```

### 配置环境变量

```bash
# agiros-loong
source /opt/agiros/loong/setup.bash # 只在当前终端有效
echo " source /opt/agiros/loong/setup.bash" >> ~/.bashrc # 在所有终端都有效
# 使配置生效
source ~/.bashrc
```

## 测试AGIROS是否安装成功
使用turtlesim demo测试AGIROS的话题通信功能。

### 打开一个终端，启动小乌龟

```bash
# 若未配置全局环境变量，则需要在每个终端source一下
source /opt/agiros/loong/setup.bash 
agiros run turtlesim turtlesim_node
```
此时，可以看到屏幕上出现了一只小乌龟。

### 打开另一个终端，启动小乌龟控制程序

```bash
# 若未配置全局环境变量，则需要在每个终端source一下
source /opt/agiros/loong/setup.bash 
agiros run turtlesim turtle_teleop_key
```

此时，可以通过键盘控制小乌龟。



