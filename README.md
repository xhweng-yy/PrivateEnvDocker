# PrivateEnvDocker
## 1.1.无外网安装docker
通过已经下载的docker安装包，在目标服务器上进行安装
 
### 1.1.1 解压缩docker安装包
tar xzvf docker-19.03.11.tgz
cp docker/* /usr/bin/
### 1.1.2 编写服务
`vim /usr/lib/systemd/system/docker.service`

```
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
After=network-online.target firewalld.service
Wants=network-online.target
[Service]
Type=notify
ExecStart=/usr/bin/dockerd
ExecReload=/bin/kill -s HUP $MAINPID
LimitNOFILE=infinity
LimitNPROC=infinity
TimeoutStartSec=0
Delegate=yes
KillMode=process
Restart=on-failure
StartLimitBurst=3
StartLimitInterval=60s
[Install]
WantedBy=multi-user.target
```
### 1.1.3 设置开机自启
systemctl daemon-reload
systemctl start docker && systemctl enable docker
### 1.1.4查看docker安装信息
docker info//systemctl docker status 

### 1.1.1 安装docker compose
将docker compose 离线安装包docker-compose-Linux-x86_64上传至服务器，在安装包目录下执行以下命令：

```

mv docker-compose-linux-x86_64 /usr/local/bin/docker-compose 

chmod +x /usr/local/bin/docker-compose

docker-compose -v

```
如出现docker-compose 命令不存在
 可执行下列命令，增加链接：

sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
到这里就安装完成了。


验证说明：
- 1、将准备好的docker-compose文件复制到/usr/local/bin/
- 2、给文件授权
- 3、使用docker加载安装包
- 4、运行docker-compose
- 5、查看安装好的docker-compose版本：docker-compose -v
 
