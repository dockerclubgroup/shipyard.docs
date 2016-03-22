---
name: Docker安装
---

# 基于Docker的安装使用


## 3.1 首次部署脚本

```sh
$ curl -sSL https://dockerclub.net/deploy | bash -s
``` 

- ACTION: 可以使用的指令 (deploy, upgrade, node, remove)
1. DISCOVERY: 集群系统采用Swarm进行采集和管理(在节点管理中可以使用‘node’)
2. IMAGE: 镜像，默认使用shipyard的镜像
3. PREFIX: 容器名字的前缀
4. SHIPYARD_ARGS: 容器的常用参数
5. TLS_CERT_PATH: TLS证书路径
6. PORT: 主程序监听端口 (默认端口: 8080)
7. PROXY_PORT: 代理端口 (默认: 2375)
        
## 3.2 脚本可选项

- 如果你要自定义部署，请参考以下规范
        1. 部署action：指令有效变量
        2. deploy: 部署新的shipyard实例
        3. upgrade: 更新已存在的实例（注意：你要保持相同的系统环境、变量来部署同样的配置）
        4. node: 使用Swarm增加一个新的node
        5. remove: 删除已存在的shipyard实例（容器） 
        
## 3.3 镜像使用

- 你可以采取规范的镜像来部署实例，比如以下的测试版本，你也已这样做

```sh
$  curl -sSL https://dockerclub.net/deploy | IMAGE=shipyard/shipyard:test bash -s
``` 

## 3.4 前缀使用

- 你可以定义你想要的前缀，比如

```sh
$  curl -sSL https://dockerclub.net/deploy | PREFIX=shipyard-test bash -s
``` 
    

## 3.5 参数使用

- 这里增加一些shipyard运行参数，你可以像这样进行调整：

```sh
$      curl -sSL https://dockerclub.net/deploy | \
        SHIPYARD_ARGS="--ldap-server=ldap.example.com" \
        --ldap-autocreate-users" bash -s
``` 

## 3.6TLS证书使用

- 启用TLS对组建进行部署，包括代理（proxy）、swarm集群系统、shipyard管理平台的配置，这是一个配置规范。证书必须采用以下命名规范：
        1. ca.pem: 安全认证证书
        2. server.pem: 服务器证书
        3. server-key.pem: 服务器私有证书
        4. cert.pem: 客户端证书
        5. key.pem: 客户端证书的key
- 注意：证书将被放置在一个docker容器中，并在各个组成部分之间共享。如果需要调试，可以将此容器连接到调试容器。数据容器名称为前缀的证书。

```sh
$  docker run --rm \
    -v $(pwd)/certs:/certs \
    ehazlett/certm \
    -d /certs \
    bundle \
    generate \
    -o shipyard \
    --host proxy \
    --host 127.0.0.1
```
    

- 你也可以按如下指令来部署系统

```sh
$    curl -sSL https://dockerclub.net/deploy | TLS_CERT_PATH=$(pwd)/certs bash -s
``` 
      
## 3.7增加一个部署节点

- shipyard节点部署脚本将自动的安装key/value存储系统（etcd系统）。增加一个节点到swarm集群，你可以使用以下的节点部署脚本

```sh
$  curl -sSL https://dockerclub.net/deploy | ACTION=node  DISCOVERY=etcd://10.0.1.10:4001 bash -s
```
        
- 注意：10.0.1.10这个ip地址你需要修改为你的首次初始化shipyard系统的主机地址

## 3.8删除shipyard系统

```sh
$  curl -sSL https://dockerclub.net/deploy | ACTION=remove bash -s
```
   
    

    


