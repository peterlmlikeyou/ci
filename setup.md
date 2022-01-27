# CI 方案概述

# 安装 Jenkins Master

## Step1 - 创建新帐户

从 IT 那边拿到新电脑之后，如果 IT 没有创建 ci 帐户，需要创建 ci 帐户:

 - 以 root 帐户登录系统
 - 创建新帐户 ci/wifici

## Step2 - 安装　Ｄocker

1. sudo apt-get update
3. sudo apt install docker.io

参考:　https://docs.docker.com/engine/install/ubuntu/

## Step3 - 安装 Jenkins

在 docker 中安装　Jenkins:　sudo docker run -p 8080:8080 -v /home/ci/jenkins:/var/jenkins_home jenkinsci/blueocean

参考:

 - https://www.jenkins.io/doc/book/installing/docker/
 - https://hub.docker.com/r/jenkinsci/blueocean

## Step4 - 安装　Jenkins 插件



# 安装 Jenkins Build Server

# 安装 Test Server

# 参考资料

　-　https://docs.docker.com/engine/install/ubuntu/
　-　
