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

在 docker 中安装　Jenkins:　sudo docker run -p 8080:8080 jenkinsci/blueocean

参考:

 - https://www.jenkins.io/doc/book/installing/docker/
 - https://hub.docker.com/r/jenkinsci/blueocean

## Step4 - 安装　Jenkins 插件

安装下述插件：

 - allure
 - Publish Over CIFS
 - pipeline 相关插件
 - metersphere，下载安装：https://github.com/metersphere/jenkins-plugin/releases/tag/v1.17.0
 - SSH
 - scp
 - jira
 - 

## Step5 - 如果为主控节点，则配置从节点

步骤：

 - Manage Jenkins -> Global Tool Configuration -> 增加 Allure Commandline
 - Manage Jenkins -> Manage Nodes and Clouds -> Add node 增加一个节点

节点配置方法：

  - 远程工作目录 - 配置远程机器上的工作目录
  - 标签
  - 启动方式 - 选择 SSH
  - 节点属性 - 选择工具位置

# 安装 Jenkins Slave

因为 Jenkins Master 通过 SSH 登录 Slave 节点，因此需要确保 Slave 节点的 SSH 服务开启，开启法：

 - sudo apt-get install openssh-server
 - sudo /etc/init.d/ssh start
 - sudo service ssh status 查看开启状态

# 安装 Jenkins Build Server

# 安装 Test Server

# 参考资料

　-　https://docs.docker.com/engine/install/ubuntu/
　-　

# CI 优化

 - 测试计划 <-> 测试用例 <-> 生成流水线 <-> 测试用例分发 <-> 测试 <-> 测试结果生成
 - 独立的编译服务器
 - 测试管理
 - 测试文档
 - 测试框架重构
