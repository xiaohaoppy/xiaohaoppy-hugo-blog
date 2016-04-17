+++
date = "2016-04-14T11:36:45+08:00"
title = "kbe编译镜像"
categories = ["kbengine"]
tags = ["kbe"]
toc = true
+++

# 镜像地址

https://github.com/xiaohaoppy/KBE_BUILD_EVN

# 如何使用
```
gir clone https://github.com/xiaohaoppy/KBE_BUILD_EVN.git

cd KBE_BUILD_EVN

docker build -t xiaohaoppy/kbe-build-env .

docker run -v /home/kbengine/kbe/bin:/kbengine/kbe/bin xiaohaoppy/kbe-build-env
```
