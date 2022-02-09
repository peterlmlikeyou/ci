# CI 方案概述

# 安装 Jenkins Master

## 创建新帐户

从 IT 那边拿到新电脑之后，如果 IT 没有创建 ci 帐户，需要创建 ci 帐户:

 - 以 root 帐户登录系统
 - 创建新帐户 ci/wifici

## 安装　Ｄocker

1. sudo apt-get update
3. sudo apt install docker.io

参考:　https://docs.docker.com/engine/install/ubuntu/

## 安装 Jenkins

在 docker 中安装　Jenkins:　sudo docker run -p 8080:8080 jenkinsci/blueocean

**sudo docker run -u 0 -p 8080:8080 -v $HOME/jenkins:/var/jenkins_home jenkinsci/blueocean**

参考:

 - https://www.jenkins.io/doc/book/installing/docker/
 - https://hub.docker.com/r/jenkinsci/blueocean

## 安装　Jenkins 插件

安装下述插件：

 - allure
 - Publish Over CIFS
 - pipeline 相关插件
 - metersphere，下载安装：https://github.com/metersphere/jenkins-plugin/releases/tag/v1.17.0
 - SSH
 - scp
 - jira
 - Jfrog artifactory

## 配置从节点

步骤：

 - Manage Jenkins -> Global Tool Configuration -> 增加 Allure Commandline
 - Manage Jenkins -> Manage Nodes and Clouds -> Add node 增加一个节点

节点配置方法：

  - 远程工作目录 - 配置远程机器上的工作目录
  - 标签
  - 启动方式 - 选择 SSH
  - 节点属性 - 选择工具位置

# 安装 Jenkins Slave

## 启动 SSH 服务

因为 Jenkins Master 通过 SSH 登录 Slave 节点，因此需要确保 Slave 节点的 SSH 服务开启，开启法：

 - sudo apt-get install openssh-server
 - sudo /etc/init.d/ssh start
 - sudo service ssh status 查看开启状态

如果 SSH Server 未启动， 则 Master 连接 Slave 时会报 "SSH Connection Refused" or "SSH Connection Closed" 错误。


## 安装 Java

Master 连上 Slave 之后会使用 Java，因此需要安装 JDK：

 - sudo apt install openjdk-17-jdk

## pytest

 - pip install pytest

## allure-pytest

 - pip install allure-pytest

## python-pytest

 - sudo apt install python-pytest

**注意，生成 allure 报告流水线语法一定不能错，不然无法生成报告，发现无法生成报告时可考虑找一个能生成报告的写法 copy 过来**

# 安装 Jenkins Build Server

## 安装工具链

可通过 scp 在 linux 机器之间传输

## 找 Steven 为 itester 添加 ssh key

## 安装 make

## install dependency

 - sudo dpkg --add-architecture i386
 - sudo apt-get update
 - sudo apt-get install build-essential cmake python3 python3-pip doxygen ninja-build libc6:i386 libstdc++6:i386 libncurses5-dev lib32z1 -y

# Install Metersphere

## install

see: https://metersphere.io/docs/installation/online_installation/

## Admin account

admin/********

# 安装 Test Server

## appium

## google driverchrome

## flashing tools

# 参考资料

　-　https://docs.docker.com/engine/install/ubuntu/
　-　

# CI 优化

 - 测试计划 <-> 测试用例 <-> 生成流水线 <-> 测试用例分发 <-> 测试 <-> 测试结果生成
 - 独立的编译服务器
 - 测试管理
 - 测试文档
 - 测试框架重构

# Jekins Pipeline

CI
.. code::

pipeline {
    agent { label 'smoke'} 

    stages {
        stage('Build') { 
            steps {
                sh 'echo "workspace=$WORKSPACE"'
                sh 'echo "clean workspace"'
                sh 'rm -rf *'
                sh 'echo "clone auto test script"'
                sh 'git clone "ssh://itester@192.168.0.46:29418/wifi/auto_test"'
                sh 'echo "mpb"'
                sh '${WORKSPACE}/auto_test/tools/ci/jobs/jobs_mpb.sh mpb freertos 3.0 ${gerrit_numbers}'
                sh 'echo "build"'
                sh '${WORKSPACE}/auto_test/tools/ci/jobs/jobs_build.sh'
            }
        }

        stage('Flash') { 
            steps {
                sh 'echo "flash"'
                //sh '${WORKSPACE}/auto_test/tools/ci/jobs/jobs_flash.sh'
            }
        }

        stage('Verify') { 
            steps {
                sh 'echo "verify"'
                sh '${WORKSPACE}/auto_test/tools/ci/jobs/jobs_verify.sh'
            }
        }
    }
    post('Results') {
        always {
            script {
                allure includeProperties: false, jdk: '', report: 'allure_report', results: [[path: 'allure_results']]
            }
        }
    }
}
