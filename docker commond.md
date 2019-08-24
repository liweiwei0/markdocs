## <p align='center'>docker 命令</p>

### docker命令
- docker --version | -v
  > 查看版本

- docker build -t pyhello .
  > 使用此目录的 Dockerfile 创建镜像

- docker run -d -p 4000:80 pyhello
  > -d 后台分离模式下运行

  > -p 指定端口映射 本机端口:容器端口
  
- docker ps [-a|-f|-n|-l|-q|-s]
  > 查看所有正在运行的容器的列表

  > -a 查看所有容器的列表，甚至包含未运行的容器
  
- docker stop <hash>
  > 平稳地停止指定的容器 hash是容器的ID
  
- docker kill <hash>
  > 强制关闭指定的容器
  
- docker rm [-f] <hash>
  > 从此机器中删除指定的容器

  > -f 强制删除
  
  > docker rm $(docker ps -a -q) 从此机器中删除所有容器

- docker rmi [-f] <imagename>
  > 从此机器中删除指定的镜像

  > -f 强制删除
  
  > docker rmi $(docker images -q) 从此机器中删除所有镜像
  
- docker images -a|-f|-q
  > 所有的镜像

  > -a 查看所有镜像的列表

- docker login
  > 使用您的 Docker 凭证登录此 CLI 会话

- docker tag <image> username/repository:tag
  > 标记 <image> 以上传到镜像库

- docker run username/repository:tag
  > 运行镜像库中的镜像

### all command
```bash
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container’s changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container’s filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container’s filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes
```
  
### docker Management Command

- docker image COMMAND
  > Manage images

  ```bash
  build       Build an image from a Dockerfile
  history     Show the history of an image
  import      Import the contents from a tarball to create a filesystem image
  inspect     Display detailed information on one or more images
  load        Load an image from a tar archive or STDIN
  ls          List images
  prune       Remove unused images
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rm          Remove one or more images
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  ```

- docker container COMMAND
  > Manage containers

  ```bash
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container’s changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container’s filesystem
  exec        Run a command in a running container
  export      Export a container’s filesystem as a tar archive
  inspect     Display detailed information on one or more containers
  kill        Kill one or more running containers
  logs        Fetch the logs of a container
  ls          List containers
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  prune       Remove all stopped containers
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  run         Run a command in a new container
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes
  ```

- docker service COMMAND
  > Manage services

  ```bash
  create      Create a new service
  inspect     Display detailed information on one or more services
  logs        Fetch the logs of a service or task
  ls          List services
  ps          List the tasks of one or more services
  rm          Remove one or more services
  rollback    Revert changes to a service's configuration
  scale       Scale one or multiple replicated services
  update      Update a service
  ```
  
- docker volume COMMAND
  > Manage volumes

  ```bash
  create      Create a volume
  inspect     Display detailed information on one or more volumes
  ls          List volumes
  prune       Remove all unused local volumes
  rm          Remove one or more volumes
  ```

- docker builder COMMAND
  > Manage builds

  ```bash
  prune       Remove build cache
  ```
  
- docker config COMMAND
  > Manage Docker configs

  ```bash
  create      Create a config from a file or STDIN
  inspect     Display detailed information on one or more configs
  ls          List configs
  rm          Remove one or more configs
  ```

- docker network COMMAND
  > Manage networks

  ```bash
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks
  ```

- docker node COMMAND
  > Manage Swarm nodes

  ```bash
  demote      Demote one or more nodes from manager in the swarm
  inspect     Display detailed information on one or more nodes
  ls          List nodes in the swarm
  promote     Promote one or more nodes to manager in the swarm
  ps          List tasks running on one or more nodes, defaults to current node
  rm          Remove one or more nodes from the swarm
  update      Update a node
  ```

- docker plugin COMMAND
  > Manage plugins

  ```bash
  create      Create a plugin from a rootfs and configuration. Plugin data directory must contain config.json and rootfs directory.
  disable     Disable a plugin
  enable      Enable a plugin
  inspect     Display detailed information on one or more plugins
  install     Install a plugin
  ls          List plugins
  push        Push a plugin to a registry
  rm          Remove one or more plugins
  set         Change settings for a plugin
  upgrade     Upgrade an existing plugin
  ```

- docker secret COMMAND
  > Manage Docker secrets

  ```bash
  create      Create a secret from a file or STDIN as content
  inspect     Display detailed information on one or more secrets
  ls          List secrets
  rm          Remove one or more secrets

  ```
  
- docker stack COMMAND
  > Manage Docker stacks

  ```bash
  deploy      Deploy a new stack or update an existing stack
  ls          List stacks
  ps          List the tasks in the stack
  rm          Remove one or more stacks
  services    List the services in the stack
  ```

- docker swarm COMMAND
  > Manage swarm

  ```bash
  ca          Display and rotate the root CA
  init        Initialize a swarm
  join        Join a swarm as a node and/or manager
  join-token  Manage join tokens
  leave       Leave the swarm
  unlock      Unlock swarm
  unlock-key  Manage the unlock key
  update      Update the swarm
  ```

- docker trust COMMAND
  > Manage trust on Docker images

- docker system COMMAND
  > Manage Docker

  ```bash
  df          Show docker disk usage
  events      Get real time events from the server
  info        Display system-wide information
  prune       Remove unused data
  ```

### docker 发布镜像
- docker login
  > 登陆
- docker tag image username/repository:tag
  > 标记镜像 运行 docker images 以查看新标记的镜像

  ```bash
  docker tag pyhello 2622026762/pyhello:test
  ```
  
- docker push username/repository:tag
  > 发布镜像 将已标记的镜像上传到镜像仓库

  ```bash
  docker push 2622026762/pyhello:test
  ```
  
### docker 拉取镜像
- docker run -p 4000:80 username/repository:tag
  > 如果镜像在机器本地不可用，Docker 将从镜像仓库中拉取它。

  > 如果您未指定这些命令中的 :tag 部分，在进行构建和运行镜像时，将使用标签 :latest 。Docker 将使用在未指定标签的情况下运行的镜像的最新版本（可以不是最新镜像）。