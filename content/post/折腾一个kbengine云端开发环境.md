+++
date = "2016-05-18T10:39:13+08:00"
title = "折腾一个kbengine云端开发环境"
categories = ["kbengine"]
tags = ["kbe"]
toc = true
+++

**docker搭建cloud9 ide 并配置kbengine开发环境**

    随着云技术的发展，各种基于云端的IDE也相继出现。相比于传统的IDE，云端IDE可以让多个程序员同时在不同的设备上查看并编辑代码，大大提升工作协同和效率。
# 启动一个cloud9容器
使用kdelfour/cloud9-docker镜像
```
docker run -it -d -p 80:80 kdelfour/cloud9-docker
```
浏览器访问http://192.168.59.103:80  
![](../img/cloud9_111.png)



# 构建kbengine开发环境

    观看docker镜像的构建文件，该镜像安装了build-essential g++ curl libssl-dev apache2-utils git libxml2-dev sshfs supervisor 继续配置kbe环境
    
```
apt-get update
apt-get install mysql-server mysql-client
apt-get install libmysqlclient-dev
```

# 下载kbengine

```
git init
git remote add githubhttps https://github.com/kbengine/kbengine.git
git pull githubhttps master
```

# 编译kbengine

```
cd kbe/src
make
```
# 配置数据库

```
    mysql> create database kbe;
	mysql> use mysql 
	mysql> delete from user where user=''; 
	mysql> FLUSH PRIVILEGES;
	mysql> grant all privileges on *.* to kbe@'%' identified by 'kbe';
	mysql> grant select,insert,update,delete,create,drop on *.* to kbe@'%' identified by 'kbe';
	mysql> FLUSH PRIVILEGES
```
# 启动kbengine服务器

```
cd assets/
sh start_server.sh
```
**最后效果**  
![](../img/cloud9_222.png)
