+++
date = "2016-04-16T19:26:35+08:00"
title = "docker中编译ngrok"
categories = ["ngrok"]
tags = ["ngrok"]
toc = true
+++

# 使用官方golang镜像
```
docker run -i -t golang /bin/bash
```
运行完直接进入容器

# 下载ngrok

```
cd /
git clone https://github.com/tutumcloud/ngrok.git /ngrok
```

# 编译ngrok
```
export GOPATH=/ngrok/
export NGROK_DOMAIN="ngrok.me" #域名

openssl genrsa -out rootCA.key 2048 #生成密钥
openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$NGROK_DOMAIN" -days 5000 -out rootCA.pem
openssl genrsa -out server.key 2048
openssl req -new -key server.key -subj "/CN=$NGROK_DOMAIN" -out server.csr
openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 5000
cp rootCA.pem assets/client/tls/ngrokroot.crt
cp server.crt assets/server/tls/snakeoil.crt
cp server.key assets/server/tls/snakeoil.key
GOOS=windows GOARCH=amd64 make release-client release-server #编译 生成win版
```
# 退出容器导出

```
docker cp <容器ID>:/ngrok/bin/windows_amd64/ /c/User/ngrok/
```
# 修改host文件
添加 127.0.0.1    ngrok.me

# 启动ngrokd
```
ngrokd -domain="ngrok.me" -httpAddr=":8080" -httpsAddr=":8081"
```
# 测试客户端 
```
ngrok -config ngrok.cfg start baseapp loginapp
```


# 测试成功
```
ngrok                                                                                                                                                   (Ctrl+C to quit)

Tunnel Status                 online
Version                       1.7/1.7
Forwarding                    tcp://ngrok.me:30013 -> 127.0.0.1:30013
Forwarding                    tcp://ngrok.me:30015 -> 127.0.0.1:30015
Web Interface                 127.0.0.1:4040
# Conn                        0
Avg Conn Time                 0.00ms
```