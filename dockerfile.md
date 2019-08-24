## Dockerfile

### Dockerfile文件
基于dockerfile构建docker镜像时，默认情况下，当前的工作目录被称为构建上下文，我们也可以使用(-f)指定Dockerfile在不同的位置。无论dockerfile实际存在于哪里，当前目录中包含的文件和目录及其递归内容都将作为构建的上下文发送到dockerd daemon进程。

1. Dockerfile中所用的所有文件一定要和Dockerfile文件在同一级父目录下，可以为Dockerfile父目录的子目录
2. Dockerfile中相对路径默认都是Dockerfile所在的目录
3. Dockerfile中一定要惜字如金，能写到一行的指令，一定要写到一行，原因是分层构建，联合挂载这个特性。Dockerfile中每一条指令被视为一层
4. Dockerfile中指明大写（约定俗成）

### .dockerignore文件
为了避免在编译镜像时一些无关紧要的文件，我们可以采用.dockerignore文件来排除文件和目录

### 指令
- FROM 
  > 指定基础镜像，必须是第一条指令。尽可能的使用官方仓库存储的镜像作为基础镜像。官方建议使用 Alpine，它大小仅5mb左右，麻雀虽小五脏俱全，用户态工具基本都有。

  > 如果不以任何镜像为基础，那么写法为：FROM scratch。

  ```bash
  FROM <image>
  FROM <image>:<tag>
  FROM <image>:<digest> 
  三种写法，其中<tag>和<digest> 是可选项，如果没有选择，那么默认值为latest
  ```
  
  > 建议：私有registry存在时，可以通过官方镜像from下来自己维护，可以自定义调整时区、基础命令等
  
- MAINTAINER
  > 为镜像指定标签，新版docker中使用LABEL指明

  ```bash
  MAINTAINER <name>
  ```
  
- LABEL
  > 为镜像指定标签, label标签以键值对的形式出现，如果包含空格请用""扩起来。标签对象必须唯一，否则后者会覆盖前者。键可以包含 .、-、a-zA-Z、0-9。

  ```bash
  LABEL <key>=<value> <key>=<value> <key>=<value> ...
  ```
  
  ```bash
  # Set one or more individual labels
  LABEL maintainer="Yichen Wang <wangycc1028@gmail.com>" \
       reference="https://github.com/wangycc/jumpserver" \
       nodejs=5.12.0 \
       tengine=2.2.0
  ```
  
  > 说明：LABEL会继承基础镜像种的LABEL，如遇到key相同，则值覆盖
  
  > 建议: 可以通过label标记项目仓库地址，维护人联系方式、依赖的版本等信息

- RUN
  > 运行指定的命令，最常见的应该是安装软件包和一些shell命令。

  > RUN是构件容器时就运行的命令以及提交运行结果
  
  ```bash
  RUN <command>
  RUN ["executable", "param1", "param2"]
  ```
  
  > 如 RUN apk --no-cache add curl git ....，我们可以通过 \ 分隔成多行便于查看软件列表的变更。
  
  ```bash
  RUN apk --no-cache update && \
    apk --no-cache add curl \
    git \
    docker \
    nodejs 
  ```
  
  > 建议：多个脚本命令通过&&符号写在一个run指令中，可以有效减少layer数量。通过"\\"分割行，可以方便预览命令变更。
  
- CMD
  > 容器启动时要运行的命令，CMD是容器启动时执行的命令，在构建时并不运行，构建时仅仅指定了这个命令到底是个什么样子

  > 如果你的镜像用于中间件 Server，CMD 的形式一般都是 CMD [“executable”, “param1”, “param2”…]。如 CMD ["apache2","-DFOREGROUND"]。

  > CMD 还在大多数情况以交互式的方式出现。如 CMD ["python"]，当你执行 docker run -it python 的时候，将进入 shell 的交互模式。
  
  > CMD 很少以 CMD [“param”, “param”] 协同 ENTRYPOINT 工作，除非我们很清楚它们俩的运行机制。

  ```bash
  CMD ["executable","param1","param2"]
  CMD ["param1","param2"]
  CMD command param1 param2
  ```
  - 第三种比较好理解了，就时shell这种执行方式和写法
  - 第一种和第二种其实都是可执行文件加上参数的形式
  
  ```bash
  CMD [ "sh", "-c", "echo $HOME" ]
  CMD [ "echo", "$HOME" ]
  ```
  
  > 补充细节：这里边包括参数的一定要用双引号，就是",不能是单引号。千万不能写成单引号。原因是参数传递后，docker解析的是一个JSON array
    
- EXPOSE
  > 暴漏容器运行时的监听端口给外部，但是EXPOSE并不会使容器访问主机的端口，如果想使得容器与主机的端口有映射关系，必须在容器启动的时候加上 -P参数。应该尽量使用应用程序通用的传统端口，如 Apache Web 服务器使用 EXPOSE 80 等。这个指令只是声明标记，具体不会在创建容器时被应用。

  ```bash
  EXPOSE <port>/<tcp/udp>
  ```
  
  > 建议: dockerfile中通过EXPOSE 标记服务会listen的端口
  
- ENV
  > 设置环境变量，常用于为应用程序提供必要的环境变量以及版本号的设置

  ```bash
  ENV <key> <value>
  ENV <key>=<value> ...
  ```
  
  > 在dockerfile中使用变量的方式
  - $varname
  - ${varname}
  - ${varname:-default value}
  - $(varname:+default value}
  
  第一种和第二种相同
  
  第三种表示当变量不存在使用-号后面的值
  
  第四种表示当变量存在时使用+号后面的值（当然不存在也是使用后面的值）
  
- ADD
  > 复制命令，把文件复制到镜像中。如果把虚拟机与容器想象成两台linux服务器的话，那么这个命令就类似于scp，只是scp需要加用户名和密码的权限验证，而ADD不用。
  
  ```bash
  ADD <src>... <dest>
  ADD ["<src>",... "<dest>"]
  ```
  
  > 路径的填写可以是容器内的绝对路径，也可以是相对于工作目录的相对路径，推荐写成绝对路径
  
  > 可以是一个本地文件或者是一个本地压缩文件，还可以是一个url
  
  > 如果把写成一个url，那么ADD就类似于wget命令
  
  ```bash
  ADD test relativeDir/ 
  ADD test /relativeDir
  ADD http://example.com/foobar /
  ```
  
  > 注意：src为一个目录的时候，会自动把目录下的文件复制过去，目录本身不会复制。如果src为多个文件，dest一定要是一个目录
 
  > 因为镜像大小很重要，故用 ADD 远程 URL 提取包是不被鼓励的，因该使用 curl 或 wget 替代。这样，能够减小镜像的层数。例如，你应该避免这样做：
  
  ```bash
  ADD http://example.com/big.tar.xz /usr/src/things/
  RUN tar -xJf /usr/src/things/big.tar.xz -C /usr/src/things
  RUN make -C /usr/src/things all
  ```
  
  > 而是：
  
  ```bash
  RUN mkdir -p /usr/src/things \
    && curl -SL http://example.com/big.tar.xz \
    | tar -xJC /usr/src/things \
    && make -C /usr/src/things all
  ```
  
- COPY
  > 复制命令。COPY只支持将本地文件复制到容器中。

  ```bash
  COPY <src>... <dest>
  COPY ["<src>",... "<dest>"]
  ```
  
  > 如果在Dockerfile中使用不用的文件，那么COPY它们可以单独使用。这样，特定文件的更改，将确保每一步的构建缓存无效，如：
  
  ```bash
  COPY requirements.txt /tmp/
  RUN pip install --requirement /tmp/requirements.txt
  COPY . /tmp/
  ```
  
  > 将COPY . /tmp/ 放在后面，这能够使 RUN 的缓存无效的数量减少。
  
  > 对于不需要ADD tar 自动提取功能的其他项目（文件，目录），我们应该始终使用 COPY。
  
- ENTRYPOINT
  > 启动时的默认命令

  ```bash
  ENTRYPOINT ["executable", "param1", "param2"]  
  ENTRYPOINT command param1 param2
  ```
  
  > ENTRYPOINT的最好的用途时设置镜像的主命令，用 CMD 作为参数，这样就可以是镜像像命令一样运行，在容器启动时，我们只需要覆盖CMD参数即可。如:
  
  > 如果我们在Dockerfile中同时写了ENTRYPOINT和CMD，并且CMD指令不是一个完整的可执行命令，那么CMD指定的内容将会作为ENTRYPOINT的参数
  
  > CMD和ENTRYPOINT共存时，CMD会被当成ENTRYPOINT的参数传入,比如:
  
  ```bash
  ENTRYPOINT ["python"]
  CMD ["--help"]
  ```
  
  > 当容器运行时候我们可以覆盖CMD指令，比如:
  
  ```bash
  docker run python -c "import sys ;print sys.version"
  #-c "import sys ;print sys.version" 会覆盖掉--help参数。
  ```
  
  > ENTRYPOINT 也可以于脚本组合使用，如一个 Postgres Official Image 的例子。：
  
  ```bash
  #!/bin/bash
  set -e

  if [ "$1" = 'postgres' ]; then
    chown -R postgres "$PGDATA"

    if [ -z "$(ls -A "$PGDATA")" ]; then
        gosu postgres initdb
    fi

    exec gosu postgres "$@"
  fi

  exec "$@"
  ```
  
  > 注：此脚本使用的 exec bash 命令 ，使最终运行的应用程序成为容器的 PID 1。这允许应用程序接收发送到容器任何 Unix 信号。将脚本复制到容器，并通过 ENTRYPOINT 开始运行：
  
  ```bash
  COPY ./docker-entrypoint.sh /
  ENTRYPOINT ["/docker-entrypoint.sh"]
  ```
  
  > 此脚本允许用户以多种方式与 Postgres 进行交互。它可以简单地启动Postgres：
  
  ```bash
  $ docker run postgres
  ```
  
  > 或者，它可以用于运行 Postgres 并将参数传递给服务器：
  
  ```bash
  $ docker run postgres postgres --help
  ```
  
  > 它也可以用来启动一个完全不同的工具，比如 Bash：
  
  ```bash
  $ docker run --rm -it postgres bash
  ```
  
  > 建议：在业务的dockerfile中用entrypoint作为镜像的主命令，CMD作为主命令默认的flag
  
- VOLUME
  > 实现挂载功能，可以将宿主机目录挂载到容器中

  > VOLUME 指令应该用于如下内容：任何类型的数据库存储区域、配置存储、容器创建的文件或目录。
  
  ```bash
  VOLUME ["/data"]
  ```
  
  > 推荐：VOLUME 用于挂载镜像中那些经常变化（易变化的）或者用户可维护的部分。

- USER
  > 设置启动容器的用户，可以是用户名或UID
  
  ```bash
  USER daemo
  USER UID
  ```
  
  > 如果一个服务不需要超级权限来运行，我们可以通过 USER 切换成非 root 用户。在 Dockerfile 中用如下方式创建：
  
  ```bash
  RUN groupadd -r postgres && useradd --no-log-init -r -g postgres postgres
  USER postgres
  ```
  
  > 建议：为了减少层数和复杂度，避免频繁使用 USER 进行用户切换
  
  > 注意：如果设置了容器以daemon用户去运行，那么RUN, CMD 和 ENTRYPOINT 都会以这个用户去运行,使用这个命令一定要确认容器中拥有这个用户，并且拥有足够权限
  
- WORKDIR
  > 设置工作目录，对RUN,CMD,ENTRYPOINT,COPY,ADD生效。如果不存在则会创建，也可以设置多次

  ```bash
  WORKDIR /path/to/workdir
  ```
  > 我们使用WROKDIR作为工作路径。而不是增加复杂的命令，如 RUN cd … && do-something这样难以阅读以及排障困难和难以维护。
  
  ```bash
  COPY cli /data/apps/bin/
  WORKDIR /data/apps/bin
  ENTRYPOINT ["cli"]
  ```
  
- ARG
  > 设置变量命令，ARG命令定义了一个变量，在docker build创建镜像的时候，使用 --build-arg =来指定参数

  ```bash
  ARG <name>[=<default value>]
  ```
  