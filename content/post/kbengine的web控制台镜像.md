+++
date = "2016-05-16T16:11:09+08:00"
title = "kbengine的web控制台镜像"
categories = ["kbengine"]
tags = ["kbe"]
toc = true
+++

# 用法
### 编译镜像
```
gir clone https://github.com/xiaohaoppy/kbe-wc.git

cd kbe-wc

docker build -t xiaohaoppy/kbe-wc .
```

### 启动镜像 

```
docker run -p 8000 xiaohaoppy/kbe-wc
```
