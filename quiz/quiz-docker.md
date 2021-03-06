# Docker

## 什么是 Docker

DOcker 是一个容器化平台，它以容器的形式将您的应用程序及其所有依赖项打包在一起，以确保应用程序在任何环境中无缝运行；

Docker 容器，将一个软件包装在一个完整的文件系统中，该文件系统包含运行所需的一切：代码、系统工具、系统库等可以安装在服务器上的任何东西；

## Docker 与虚拟机的区别

Docker 不是虚拟化方法，它依赖与实际实现基于容器的虚拟化或操作系统及虚拟化的其他工具。为此，docker 最初使用 LXC 驱动程序，然后移动到 libcontainer 现在重命名为 runc。Docker 主要专注于在应用程序容器内自动部署应用程序。应用程序容器旨在打包和运行单个服务，而系统容器则设计为运行多个进程，如虚拟机。因此，Docker 被视为容器化系统上的容器管理或应用程序部署工具。

主要表现在以下几个方面：

1. 与虚拟机不同，容器不需要引导操作系统内核，因此可以在不到一秒的时间内创建容器。此功能使基于容器的虚拟化比其他虚拟化方法更加独特和可取；

2. 由于基于容器的虚拟化为主机增加了很少或没有开销，因此基于容器的虚拟化具有接近本机的性能；
3. 对于基于容器的虚拟化，与其他虚拟化不同，不需要其他软件；
4. 主机上的所有容器共享主机的调度程序，从而节省了额外资源的需求；
5. 与虚拟机映像相比，容器状态（Docker 或 LXC 映像）的大小很小，因此容器映像很容易分发；
6. 容器中的资源管理是通过 cgroup 实现的。Cgroups 不允许容器消耗比分配给它们更多的资源。虽然主机的所有资源都在虚拟机中可见，但无法使用。这可以通过在容器和主机上同时运行 top 或 htop 来实现。所有环境的输出看起来都很相似；

## CI(持续集成)服务器的功能是什么

## 什么是 Docker 镜像

## 什么是 Docker 容器

## Docker 容器有几种状态

运行，已暂停，重新启动，已退出

## Dockerfile 中常见的指令有哪些

1. FROM：指定基础镜像
2. LABEL： 功能是为镜像指定标签
3. RUN： 运行指定的命令
4. CMD：容器启动时要运行的命令
5. EXPOSE：声明容器的服务商品（仅仅是声明）
6. ENV：声明容器环境变量
7. ADD：拷贝文件或目录到容器中，如果是 URL 或压缩包便会自动下载或自动解压；
8. COPY：拷贝文件或目录到容器中，跟 ADD 类似，但不具备自动下载或解压的功能；
9. ENTRYPOINT：运行容器时执行的 shell 命令；
10. VOLUME：指定容器挂载点到宿主机自动生成的目录或其他容器；
11. USER：为 RUN、CMD、和 ENTRYPOINT 执行命令指定运行用户；
12. WORKDIR：为 RUN、CMD、ENTRYPOINT、COPY 和 ADD 设置工作目录，意思为切换目录；
13. HEALTHCHECH：健康检查；
14. ARG：构建时指定的一些参数；
15. LABEL：我们使用 LABEL 按照项目，模块，许可等组织我们的镜像。我们也可以使用 LABEL 来帮助实现自动化。在 LABEL 中，我们指定一个键值对，以后可用于以编程方式处理 Dockerfile；

注意：

1. RUN 在 building 时运行，可以写多条；
2. CMD 和 ENTRYPOINT 在运行 container 时，只能写一条，如果写多条，最后一条生效；
3. CMD 在构建容器时可以被 COMMAND 覆盖，ENTRYPOINT 不会被 COMMAND 覆盖，但可以指定——entrypoint 覆盖；
4. 如果在 Dockerfile 文件中需要往镜像中导入文件，则该文件必须在 Dockerfile 所在目录或子目录中；
5. 每个目录下最好就只有一个 Dockerfile，如果有多个 Dockerfile 文件时，使用 Dockerfile 生成镜像时便需要使用“-f”来指定具体的 Dockerfile 文件；
6. 指令必须全部为大写；
7. 使用 Dockerfile 生成镜像时，保证 Dockerfile 中所需的软件、文件与 Dockerfile 在同一个目录下；

## Dockerfile 中的 ONBUILD 指令

当镜像用作另一个镜像构建的基础是，ONBUILD 指令向镜像添加将在稍后执行的触发指令。如果要构建其他镜像的基础的镜像（例如，可以使用特定于用户的配置自定义的应用程序构建环境或守护程序），这将非常有用。

## Dockerfile 中的命令 COPY 和 ADD 命令有什么区别

## Dockerfile 中的 RUN 和 CMD 命令有什么区别

## Docker 镜像和层有什么区别

镜像：Docker 镜像是由一系列只读层构建的
层：每个层代表镜像 Dockerfile 中的一条指令
重要的是，每个层只是与之前一层的一组差异层（相同的就不再放到新层中）；

## 如何在多个环境中使用 Docker

## Docker 的常用命令

```bash
docker pull  # 摘取或更新指定镜像
docker push  # 将镜像推送至远程仓库
docker rm  # 删除容器
docker rmi  # 删除镜像
docker images  # 列出也有镜像
docker ps  # 列出所有容器
```

## 如何批量删除或者停止运行的容器

```bash
docker kill/rm `docker ps -aq`
```

## 如何查看镜像支持的环境变量

```bash
docker run IMAGE env
```

## 本地的镜像文件都存放在哪里

Docker 相关的本地资源存放在/var/lib/docker/目录下

其中 container 目录存放容器信息

graph 目录存放镜像信息

aufs 目录下存放具体的镜像底层文件

## 构建 Docker 镜像应该遵循哪些原则

整体远侧上，尽量保持镜像功能的明确和内容的精简，要点包括：

1. 尽量选取满足需求但较小的基础系统镜像
2. 清理编译生成文件、安装包的缓存等临时文件
3. 安装各个软件时候要指定准确的版本号，并避免引入不需要的依赖
4. 从安全的角度考虑，应用尽量使用系统的库和依赖
5. 使用 Dockerfile 创建镜像时候要添加.dockerignore 文件或使用干净的工作目录

## 容器退出后，通过 docker ps 命令查看不到，数据会丢失么

容器退出后会处于终止（exited）状态，此时可以通过 docker ps -a 查看，其中数据不会丢失，还可以通过 docker start 来启动，只有删除容器才会清除数据。

在这里还要注意开启容器的时候是否添加了--rm 参数

## 如何临时退出一个正在交互的容器的终端，而不是终止它

按 Ctrl+p，后按 Ctrl+q，如果按 Ctrl+c 会使容器内的应用进程终止，进而会使容器终止。

## 很多应用容器默认后台运行，如何何年它们的输出和日志信息

使用 docker logs，后面跟容器的名称或者 ID 信息

## 使用 docker port 命令映射容器的端口时，系统报错 `Error: No public port 80 published for ...`是什么意思

创建镜像时 Dockerfile 要指定正确的 EXPOSE 的端口，容器启动时指定 PublishAllport=true

## 可以在一个容器中同时运行多个应用进程吗

一般不推荐在同一个容器内运行多个应用进程，如果有类似需求，可以通过额外的进程管理机制，比如 supervisord 来管理所运行的进程

## 如何控制容器占用系统资源（CPU，内存）的份额

在使用 docker create 命令创建容器或使用 docker run 创建并运行容器的时候，可以使用-c|–cpu-shares[=0]参数来调整同期使用 CPU 的权重，使用-m|–memory 参数来调整容器使用内存的大小。

## 仓库（Repository）、注册服务器（Registry）、注册索引（Index）有何关系

首先，仓库是存放一组关联镜像的集合，比如同一个应用的不同版本的镜像，注册服务器是存放实际的镜像的地方，注册索引则负责维护用户的账号，权限，搜索，标签等管理。注册服务器利用注册索引来实现认证等管理。

## Docker 的配置文件放在哪里，如何修改配置

Ubuntu 系统下 Docker 的配置文件是/etc/default/docker

CentOS 系统配置文件存放在/etc/sysconfig/docker

## 如何更改 Docker 的默认存储设置

Docker 的默认存放位置是/var/lib/docker

如果希望将 Docker 的本地文件存储到其他分区，可以使用 Linux 软连接的方式来做。

## Docker 与 LXC（Linux Container）有何不同

LXC 利用 Linux 上相关技术实现容器，Docker 则在如下的几个方面进行了改进：

1. 移植性：通过抽象容器配置，容器可以实现一个平台移植到另一个平台；
2. 镜像系统：基于 AUFS 的镜像系统为容器的分发带来了很多的便利，同时共同的镜像层只需要存储一份，实现高效率的存储；
3. 版本管理：类似于 GIT 的版本管理理念，用户可以更方面的创建、管理镜像文件；
4. 仓库系统：仓库系统大大降低了镜像的分发和管理的成本；
5. 周边工具：各种现有的工具（配置管理、云平台）对 Docker 的支持，以及基于 Docker 的 Pass、CI 等系统，让 Docker 的应用更加方便和多样化。

## Docker 与 Vagrant 有何不同

两者的定位完全不同
Vagrant 类似于 Boot2Docker（一款运行 Docker 的最小内核），是一套虚拟机的管理环境，Vagrant 可以在多种系统上和虚拟机软件中运行，可以在 Windows、Mac 等非 Linux 平台上为 Docker 支持，自身具有较好的包装性和移植性。

原生 Docker 自身只能运行在 Linux 平台上，但启动和运行的性能都比虚拟机要快，往往更适合快速开发和部署应用的场景。

## 开发环境中 Docker 与 Vagrant 该如何选择

Docker 不是虚拟机，而是进程隔离，对于资源的消耗很少，单一开发环境下 Vagrant 是虚拟机上的封闭，虚拟机本身会消耗资源
。

## 如何将一台宿主机的 Docker 环境迁移到另外一台宿主机

停止 Docker 服务，将整个 docker 存储文件复制到另外一台宿主机上，然后调整另外一台宿主机的配置即可

## Docker 容器创建后，删除了/var/run/netns 目录下的网络名字空间文件，可以手动恢复它

```bash
# 查看容器进程ID，比如1234
sudo docker inspect --format='{{. State.pid}}' $container_id
1234
# 到proc目录下，把对应的网络名字空间文件链接到/var/run/netns,然后通过正常的系统命令查看操作容器的名字空间。
```

## Docker 中的网络类型

1. host 模式：直接使用 docker 宿主机的 I 网络。如 IP 地址、网卡类型等；
2. none 模式：不会给容器进行任何网络配置。也就是说，使用这种模式的容器没有 IP 地址（只有一个回环地址）；
3. bridge 模式：docker 默认的网络配置，此模式会为每一个容器分配名称空间，可以设置 IP，但是要与 docker host 主机的虚拟网络在同一网段；通过虚拟网卡与外界通信；
4. container 模式：这种模式与已经存在的容器共有同一个 IP 地址；
5. Network：自定义网络。可以自行创建并且可以注定多种网络驱动，如 bridge、overlay 等；

## Docker 容器的跨主机网络通信

跨主机通信的两种解决方案：

overlay 网络：使用这种方法，需要事先创建一个 consul 服务，将需要跨主机通信的 docker host 加入到同一个 consul 集群中，然后再创建一个 overlay 类型的自定义网络。由于其网卡作用于是全局的，所以基于此网卡类型创建的容器就可以正常通信；

macvlan 网络：使用这种方法，首先开启网卡的混杂模式，然后配置虚拟网卡，这些虚拟网卡拥有独立的 mac 地址，可以配置 IP 地址进行通信。与 overlay 不同的是，macvlan 的作用范围是本地有效。
如果使用 macvlan 网络的方式，需要以下步骤：

首先要保证需要跨主机通信的 docker hos 是可以正常通信的；
两台 docker host 创建的虚拟网卡是在同一网段；
然后两台 docker host 基于虚拟网卡创建 macvlan 类型的网卡；
通过 macvlan 网络类型创建的容器即可通信；

## Docker 数据持久化

Docker 实现数据持久化的方式

1. Bind mount（绑定挂载）：
   创建容器时，使用“-v”选项，将本地的目录挂载到容器中。采用这种方式容器的挂载类型为 bind！

   特点：

   - Data Volume 是目录或文件，不能是没有格式化的磁盘（块设备）；
   - 容器可以读写 volume 中的数据；
   - 随源文件变化而变化；
   - volume 数据可以永久保存，即使使用它的容器已经被销毁；

   注意：

   - DockerHost 上需要被挂着的源文件或目录，必须是已经存在，否则，当做的一个目录挂着到容器中；
     默认挂载到容器内的文件，容器是有读写权限。可以在运行容器是-v 后边加“：ro” 限制容器的写入权限；
   - 可以挂载单独的文件到容器内部，使用场景：如果不想对整个目录进行覆盖，而只希望添加某个文件，就可以使用挂载单个文件；

2. Manager Volume（数据卷管理员）

   创建容器时，使用“-v“选项，只指定容器中的目录即可！采用这种方式容器的挂载类型为 volume；

   特点：

   - 随着源文件的变化而变化，跟 Bind mount 效果是一样；
   - 删除容器的操作，默认不会对 dockerhost 主机上的原文件进行删除，如果想要在删除容器是将原文件删除，可以在删除容器时添加“-v”选项，（一般情况下不建议使用，因为文件有可能被其他容器就使用）；

3. Volume container（容器与容器的数据共享）

   采用这种方式，即事先创建一个容器，专用于挂载本地的目录，然后创建容器时，使用“--volumes-from”指定挂载本地目录的容器即可（这种模式是将原本容器中挂载的所有目录都挂载到新创建的容器中）！

   这种方式也是提供 bind mount 模式和 manager volume 模式！
