---
name: 源码安装
---

# 安装golang

shipyard是基于golang开发的，如果需要源码安装调试必须先安装golang，golang安装如下：


```sh
$ wget https://storage.googleapis.com/golang/go1.4.linux-amd64.tar.gz
$ sudo tar -xzf go1.4.linux-amd64.tar.gz -C /usr/local
```
加入环境变量
```sh
$ sudo vi ~/.bashrc
 GOPATH="/YOUR/USER/HOME/go"
 GOROOT="/usr/local/go"
 PATH=$GOROOT/bin:$PATH
```
GOPATH 是 Golang 的开发目录，按照 官方文档的说明，需要有确定的目录结构：

GOPATH=/home/user/gocode
home/user/gocode/
    src/
        foo/
            bar/               (go code in package bar)
                x.go
            quux/              (go code in package main)
                y.go
    bin/
        quux                   (installed command)
    pkg/
        linux_amd64/
            foo/
                bar.a          (installed package object)
                
# 克隆代码
```sh
 git clone https://github.com/dockerclubgroup/shipyard.git 
```

注意：代码位于GOPATH的src目录，且必须放置在src下的github/shipyard目录下

# 安装nodejs依赖
```sh
$ git clone git@github.com:creationix/nvm.git ~/.nvm
$ vi ~/bashrc
加入 . ~/.nvm/nvm.sh
安装nodejs
$ nvm install v1.2.0
安装bower
$ npm install bower -g
```

# 构建并允许
```sh
$  make all
$  make testrun
```