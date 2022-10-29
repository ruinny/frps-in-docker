# frps-in-docker是什么
利用Docker快速部署Frps

> 更新时间 2022-10-29

# 使用说明

# 安装Docker
wget -qO- https://get.docker.com/ | sh

# 抽取镜像
```docker pull ruiny/frps````

frps的0.17.0和0.24.1两个版本和下个版本不兼容，如果需要可以pull这两个镜像，一般情况用上面这个命令就行
```docker pull ruiny/frps:0.24.1```
```docker pull ruiny/frps:0.17.0```

## 添加frps.ini配置文件
```bash
rm -rf /var/frp && \
mkdir /var/frp && \
mkdir /var/frp/conf && \
cd /var/frp/conf && \
wget https://raw.githubusercontent.com/ruinny/frps-in-docker/master/frps.ini && \
chmod +x frps.ini
```

#### 根据需要修改配置文件
`nano /var/frp/conf/frps.ini` 


## 启动镜像（docker run方式）
```bash
docker run --name frps --restart=always -d \
-v /var/frp/conf:/var/frp/conf \
-p 15000-15100:15000-15100 -p 7000:7000 -p 7500:7500 -p 7001:7001 -p 7080:80 -p 7443:443 \
ruiny/frps
```

## 启动镜像（docker-compose方式）
```bash
git clone https://github.com/ruinny/frps-in-docker.git
cd frps-in-docker
docker-compose up -d
```

> 说明
 - 配置文件存放在/var/frp/conf
 - 默认80和443端口映射到7080和7443，如需改回去的自己修改
 - 默认端口开放15000-15100 如果需要调整的请在frps.ini和docker端口中同时调整
 - 只适用于x64，不适用于arm
 - 适配smzdm教程 https://post.smzdm.com/p/743634/
