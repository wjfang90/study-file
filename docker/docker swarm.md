# docker swarm

docker swarm 是一个 docker 集群管理工具，跟kubernetes类似

docker swarm

优点

- 简单易用，轻量级，docker 集成

缺点

- 1.功能相对较弱，特别是在调度和自动部署方面。
- 2.社区支持和文档相对较少

kubernetes

优点

- 1.功能强大，支持多种容器编排功能，如调度、自动部署、服务发现等。
- 2.社区支持和文档丰富。
- 3.具有很好的可扩展性和兼容性，支持多种容器镜像和工具。

缺点：

- 1.相对复杂，学习和使用成本较高。
- 2.不支持Docker以外的容器运行时。

## 集群管理

docker swarm COMMAND

Commands:

- ca          Display and rotate the root CA
- init        Initialize a swarm
- join        Join a swarm as a node and/or manager
- join-token  Manage join tokens
- leave       Leave the swarm
- unlock      Unlock swarm
- unlock-key  Manage the unlock key
- update      Update the swarm

### 初始化集群

docker swarm init   执行 docker swarm init 命令的节点自动成为管理节点

Docker 主机有多个网卡，拥有多个 IP，必须使用 --advertise-addr 指定 IP

``` sh
docker swarm init --advertise-addr 192.168.99.101
```

### 加入集群

docker swarm join --token token_value ip:port

``` sh
docker swarm join \
--token SWMTKN-1-5twf8bx96sou5fty8cu51irbbwjgzhenbvw3mtyj1vtpaaj4r6-4j5q6hza0eaioogtuxi666xyu 192.168.99.101:2377
```

### 查看集群

``` sh
docker node ls  在管理节点使用 docker node ls 查看集群
```

### 离开集群

``` sh
docker swarm leave
```

### 删除集群

``` sh
docker swarm leave --force
```

## 集群中服务管理

docker service COMMAND

Commands:

- create      Create a new service
- inspect     Display detailed information on one or more services
- logs        Fetch the logs of a service or task
- ls          List services
- ps          List the tasks of one or more services
- rm          Remove one or more services
- rollback    Revert changes to a service's configuration
- scale       Scale one or multiple replicated services
- update      Update a service

### 新建服务

docker service create  

``` sh
docker service create \
    --replicas 3 \
    --name nginx_swarm_service \
    nginx:latest
```

### 查看服务

``` sh
docker service ls
```

### 更新服务

``` sh
docker service update --image nginx:1.15.8 nginx_swarm_service
```

### 伸缩服务

``` sh
docker service scale nginx_swarm_service=5
```

### 删除服务

``` sh
docker service rm nginx_swarm_service
```

## 集群中使用compose

docker service create 一次只能部署一个服务，使用 docker-compose.yml 我们可以一次启动多个关联的服务

### stack部署服务compose

docker stack [OPTIONS] COMMAND

Manage Docker stacks

Options:
      --kubeconfig string     Kubernetes config file
      --orchestrator string   Orchestrator to use (swarm|kubernetes|all)

Commands:
  deploy      Deploy a new stack or update an existing stack
  ls          List stacks
  ps          List the tasks in the stack
  rm          Remove one or more stacks
  services    List the services in the stack

``` sh
docker stack deploy nginx_stack -c docker-compose.yml
```

docker-compose.yml

``` sh compose
version: '3'

services:
  nginx:
    image: nginx:latest
    ports:
      - "8088:80"
    networks:
      - mynet
    deploy:
      replicas: 2
      placement:
        constraints:
          - node.role == manager
      restart_policy:
        condition: on-failure
networks:
  mynet:
    driver: overlay
```

``` sh
docker stack deploy nginx_stack -c docker-compose.yml
```

### stack 查看服务

``` sh
docker stack ls
 ```

### stack 删除服务

``` sh
docker stack down stack_name

docker stack down stack_name
```

## swarm 集群管理敏感数据

Docker 目前已经提供了 secrets 管理功能，用户可以在 Swarm 集群中安全地管理密码、密钥证书等敏感数据，并允许在多个 Docker 容器实例之间共享访问指定的敏感数据

注意： secret 也可以在 Docker Compose 中使用

### 创建secret

docker secret create [OPTIONS] SECRET [file|-]

docker secret create 命令以管道符的形式创建 secret

``` sh
openssl rand -base64 20 | docker secret create mysecret -

openssl rand -base64 20 | docker secret create mysqlsecret -
```

说明：

- 使用OpenSSL的rand命令生成一个20个字符的随机字符串，并将其转换为Base64编码

- | 管道符，表示将openssl生成的随机字符串作为输入

- \- 表示将openssl生成的随机字符串作为输入

``` sh
echo -n 'secret_value' | docker secret create mysercret -
```

使用 echo 命令创建secret

- 参数-n 选项来确保不输出结尾的换行符

### 查看secret

``` sh
docker secret ls
```

### 删除secret

``` sh
docker secret rm mysecret

docker secret rm mysqlsecret
```

### 创建secret 卷

没有在target 中显式的指定路径时，secret 默认通过 tmpfs 文件系统挂载到容器的 /run/secrets 目录中。

``` sh
docker service create \ 
--name myservice \
--secret source=mysqlsecret,target=/run/secrets/mysql_password \
mysql:latest
```

创建mysql服务

``` sh
docker network create -d overlay mysql_private

docker service create \
     --name mysql \
     --replicas 1 \
     --network mysql_private \
     --mount type=volume,source=mydata,destination=/var/lib/mysql \
     --secret source=mysql_root_password,target=mysql_root_password \
     --secret source=mysql_password,target=mysql_password \
     -e MYSQL_ROOT_PASSWORD_FILE="/run/secrets/mysql_root_password" \
     -e MYSQL_PASSWORD_FILE="/run/secrets/mysql_password" \
     -e MYSQL_USER="test" \
     -e MYSQL_DATABASE="test_db" \
     mysql:latest
```

## swarm 集群中管理配置数据

在 Docker 17.06 以上版本中，Docker 新增了 docker config 子命令来管理集群中的配置信息，以后你无需将配置文件放入镜像或挂载到容器中就可实现对服务的配置。

注意：config 仅能在 Swarm 集群中使用。

### 创建config

docker config COMMAND

Manage Docker configs

Commands:
  create      Create a config from a file or STDIN
  inspect     Display detailed information on one or more configs
  ls          List configs
  rm          Remove one or more configs

### 查看config

``` sh  
docker config ls
```

### 删除config

``` sh  
docker config rm myconfig
```

### 以 config 创建服务

``` sh
docker config create myredis.conf redis.conf
```

创建一个名为 myredis.conf 的 Docker 配置项，并将一个名为 redis.conf 的配置文件作为其源文件

- myredis.conf: 这是为配置项指定的名称，即 myredis.conf。

- redis.conf: 这是配置文件的源文件，即 redis.conf。它应该是一个已经存在的文件，其中包含了 Redis 的配置信息

``` sh
docker service create \
     --name myredis \          
     # --config source=myconfig,target=/etc/redis.conf \
     --config redis.conf \
     -p 6379:6379 \
     redis:latest \
     redis-server /etc/redis.conf
```

没有在 target 中显式的指定路径时，默认的 redis.conf 以 tmpfs 文件系统挂载到容器的 /config.conf

## 滚动升级

滚动升级，即在不停机的情况下，对服务进行升级。

docker service update 更新任意的配置。

--secret-add 选项可以增加一个密钥

--secret-rm 选项可以删除一个密钥

更多选项可以通过 docker service update -h 命令查看

``` sh
docker service update \
        --image nginx:latest \
        nginx
```

## 服务回退

当升级服务发生故障时，可以通过回退功能，将服务回退到之前的版本。

``` sh
docker service update --rollback nginx
```
