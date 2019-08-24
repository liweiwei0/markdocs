## <p align='center'>搭建redis集群</p>

> 一个redis集群最少三个及以上的主节点
### macOS搭建
#### 操作步骤
1. 下载redis文件 5.0.4版本 地址：http://download.redis.io/releases/redis-5.0.4.tar.gz
2. 解压
```bash
tar -zxvf redis-5.0.4.tar.gz
cd redis-5.0.4
```
3. 编译
```bash
make
```
4. 创建集群文件夹
```bash
mkdir redis-cluster
cd redis-cluster
mkdir 7000 7001 7002 7003 7004 7005
```
5. 修改个节点redis.conf配置
```bash
cp ../redis.conf 7000/
vi 7000/redis.conf
```
6. 更改内容
```json
# 端口
port 7000
# 默认ip为127.0.0.1需要改为其他节点机器可访问的ip否则创建集群时无法访问对应的端口，无法创建集群
bind 127.0.0.1
# redis后台运行
daemonize yes
# pidfile文件对应7000
pidfile redis_7000.pid
# 开启集群把注释#去掉
cluster-enabled yes
# 集群的配置配置文件首次启动自动生成
cluster-config-file nodes_7000.conf
# 请求超时默认5秒，可自行设置
cluster-node-timeout 5000
# aof日志开启有需要就开启，它会每次写操作都记录一条日志
appendonly yes
```
7. 启动个节点
```bash
src/redis-server 7000/redis.conf
src/redis-server 7001/redis.conf
src/redis-server 7002/redis.conf
src/redis-server 7003/redis.conf
src/redis-server 7004/redis.conf
src/redis-server 7005/redis.conf
```
8. 配置集群
```bash
src/redis-cli --cluster create 127.0.0.1:7000 127.0.0.1:7001 127.0.0.1:7002 127.0.0.1:7003 127.0.0.1:7004 127.0.0.1:7005 --cluster-replicas 1
```
9. 验证 进入任意一个redis节点 查看集群节点
```bash
src/redis-cli -h 127.0.0.1 -p 7000
cluster nodes
```