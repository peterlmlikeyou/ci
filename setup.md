# CI 方案概述

# 安装 Jenkins Master

## Step1 - 创建新帐户

从 IT 那边拿到新电脑之后，如果 IT 没有创建 ci 帐户，需要创建 ci 帐户:

 - 以 root 帐户登录系统
 - 创建新帐户 ci/wifici

## Step2 - 安装　Ｄocker

1. sudo apt-get update
3. sudo apt install docker.io

## Step3 - 安装 Jenkins

1. sudo apt-get update
2. sudo apt install curl
3. sudo apt install docker.io
4. 
5. curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
4. sudo apt-get update
5. sudo apt-get install jenkins
6. 
参考官网安装 Jenkins: https://www.jenkins.io/doc/book/installing/linux/

## Step3 - 
# 安装 Jenkins Build Server

# 安装 Test Server

# 安装 
