# Docker开发与部署

> Written  In 2025_07.10 __by yxl   
> Last Edited In 2025_07.10__by yxl

本文记录关于Docker的使用教程与过程记录

---

推荐教程： [Docker — 从入门到实践](https://yeasy.gitbook.io/docker_practice)

---

## 过程示例

1. 安装

按照上述推荐教程进行docker的安装。

- 镜像源示例



``` bash
$vim /etc/docker/daemon.json
#在文件中添加下面的源
{
"registry-mirrors" :
    [
        "https://docker.m.daocloud.io",
        "https://noohub.ru",
        "https://huecker.io",
        "https://dockerhub.timeweb.cloud",
        "https://docker.rainbond.cc"
]
}
```

注意，如果出现更换镜像源之后不生效的情况，可以尝试如下步骤进行刷新：

```bash
sudo systemctl daemon-reload
docker system prune -a
sudo service docker restart
```

## Docker样例

```bash
# 使用 Ubuntu 22.04 作为基础镜像
FROM ubuntu:22.04

# 设置环境变量，避免在非交互式环境中出现提示
ENV DEBIAN_FRONTEND=noninteractive


# 更新apt源并安装必要的开发工具，包括所有llama.cpp可能的依赖
RUN apt update && \
    apt install -y \
    build-essential \
    cmake \
    git \
    python3 \
    python3-pip \
    openssh-server \
    locales \
    iputils-ping \
    dnsutils  \
    curl   \
    net-tools \
    wget \
    openssh-client && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

RUN ssh-keygen -A

# 设置 SSH 服务
RUN mkdir /var/run/sshd
RUN echo 'root:123456' | chpasswd # 设置root用户的密码为docker，后续远程连接使用
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSHD 配置：允许root登录，禁用密码登录（如果您想使用SSH密钥对）
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

# 创建一个普通用户（可选，但推荐）
RUN useradd -ms /bin/bash docker1
RUN echo 'docker1:123456' | chpasswd
RUN usermod -aG sudo docker1 # 将developer用户添加到sudo组

# 设置默认用户为 root
USER root

# 设置工作目录，后续我们将主机上的llama.cpp项目挂载到这个目录
# 注意：这里只是定义一个容器内的目录，实际挂载在运行容器时指定
WORKDIR /home/docker1/workspace
# 暴露SSH端口
EXPOSE 22


# 启动 SSH 服务
CMD ["/usr/sbin/sshd", "-D"]

```

## 编译、运行

1. 编译镜像

```
docker build -t demo-dev:latest .
```
2. 启动运行

```
docker run -d -p 2222:22 --name llamacpp_dev_container llamacpp-dev:latest
```