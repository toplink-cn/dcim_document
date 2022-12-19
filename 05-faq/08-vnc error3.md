# VNC反复连接失败

点击vnc进行连接,页面会连接时间长，或者是连接上之后页面反复断开，请尝试以下方法进行解决。


  -  重制BMC （重制期间会连接不上机器稍等片刻再重新尝试连接）  
  -  给平台加上SSL证书时链接安全（已有请忽略）  
  -  升级平台至最新版 （已是最新请忽略）  
  - Ssh连接被控机器重启docker或重启consoled容器.  


重启docker：
```
Systemctl restart docker    **or**    service docker restart
```
重启consoled 容器 
```
docker restart dcim-agent-consoled
```



