+++
date = "2016-04-14T14:12:03+08:00"
title = "使用反向链接搭建公网可访问的kbe服务"
categories = ["kbengine"]
tags = ["kbe", "ngrok"]
toc = true
+++

# Ngrok 内网穿透利器  
ngrok 是一个反向代理，通过在公共的端点和本地运行的 Web 服务器之间建立一个安全的通道。ngrok 可捕获和分析所有通道上的流量，便于后期分析和重放


使用国内免费Ngrok http://qydevv.com

正式使用自行搭建ngrok服务器

ngrok开源地址 https://github.com/tutumcloud/ngrok

# 开始部署
修改kbengine配置文件

```
	<loginapp>
        <externalAddress> tunnel.qydev.com </externalAddress>
        <externalPorts_min> 30013 </externalPorts_min>		
                        			
		<externalPorts_max> 0 </externalPorts_max>
	</loginapp>	
    
    
    <baseapp>
		<backupPeriod> 500 </backupPeriod>
        <externalAddress> tunnel.qydev.com </externalAddress>
        <externalPorts_min> 30015 </externalPorts_min>					 
		<externalPorts_max> 0 </externalPorts_max>
	</baseapp>
```

ngrok配置文件


```
server_addr: "tunnel.qydev.com:4443"
trust_host_root_certs: false
tunnels: 
  loginapp:
   remote_port: 30013 
   proto:
    tcp: 30013 
  baseapp: 
    remote_port: 30015
    proto:
      tcp: 30015

```

# 启动kbe
```
sh start_server.bat
```
# 启动ngrok
```
ngrok -config ngrok.cfg start baseapp loginapp
```

这样外网就可以访问内网kbe服务了。

