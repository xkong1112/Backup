

# Deploy

## Dockerfile

### VERSION：

``` bash
VERSION
#FROM指令指定的基础image可以是官方远程仓库中的，也可以位于本地仓库
FROM <image> || FROM <image>:<tag>
```

### MAINTAINER（用来指定镜像创建者信息）

```bash
MAINTAINER <name>
```

### RUN可以运行任何被基础image支持的命令，安装软件用

```bash
RUN <command> (the command is run in a shell - `/bin/sh -c`)  
RUN ["executable", "param1", "param2" ... ]  (exec form)
```

### CMD（设置container启动时执行的操作）

设置指令，用于container启动时指定的操作。该操作可以是执行自定义脚本，也可以是执行系统命令。该指令只能在文件中存在一次，如果有多个，则只执行最后一条。

```bash
CMD ["executable","param1","param2"] (like an exec, this is the preferred form)  
CMD command param1 param2 (as a shell)
```

### ENTRYPOINT

指定的是一个可执行的脚本或者程序的路径，该指定的脚本或者程序将会以param1和param2作为参数执行。所以如果CMD指令使用上面的形式，那么Dockerfile中必须要有配套的ENTRYPOINT。

```bash
CMD ["param1","param2"] (as default parameters to ENTRYPOINT)
```

ENTRYPOINT（设置container启动时执行的操作）设置指令，指定容器启动时执行的命令，可以多次设置，但是只有最后一个有效。

```bash
ENTRYPOINT ["executable", "param1", "param2"] (like an exec, the preferred form)  
ENTRYPOINT command param1 param2 (as a shell)
```

该指令的使用分为两种情况，一种是独自使用，另一种和CMD指令配合使用。
当独自使用时，如果你还使用了CMD命令且CMD是一个完整的可执行的命令，那么CMD指令和ENTRYPOINT会互相覆盖只有最后一个CMD或者ENTRYPOINT有效。

CMD指令将不会被执行，只有ENTRYPOINT指令被执行  

```bash
CMD echo “Hello, World!”  
ENTRYPOINT ls -l
```

另一种用法和CMD指令配合使用来指定ENTRYPOINT的默认参数，这时CMD指令不是一个完整的可执行命令，仅仅是参数部分；ENTRYPOINT指令只能使用JSON方式指定执行命令，而不能指定参数。

```bash
FROM ubuntu  
CMD ["-l"]  
ENTRYPOINT ["/usr/bin/ls"]USER（设置container容器的用户）
```

设置指令，设置启动容器的用户，默认是root用户。

```bash
# 指定memcached的运行用户  
ENTRYPOINT ["memcached"]  
USER daemon  
或  
ENTRYPOINT ["memcached", "-u", "daemon"]
```

### EXPOSE（指定容器需要映射到宿主机器的端口）

设置指令，该指令会将容器中的端口映射成宿主机器中的某个端口。当你需要访问容器的时候，可以不是用容器的IP地址而是使用宿主机器的IP地址和映射后的端口。要完成整个操作需要两个步骤，首先在Dockerfile使用EXPOSE设置需要映射的容器端口，然后在运行容器的时候指定-p选项加上EXPOSE设置的端口，这样EXPOSE设置的端口号会被随机映射成宿主机器中的一个端口号。也可以指定需要映射到宿主机器的那个端口，这时要确保宿主机器上的端口号没有被使用。EXPOSE指令可以一次设置多个端口号，相应的运行容器的时候，可以配套的多次使用-p选项。

格式:

```bash
EXPOSE <port> [<port>...]
# 映射一个端口  
EXPOSE port1  
# 相应的运行容器使用的命令  
docker run -p port1 image  

# 映射多个端口  
EXPOSE port1 port2 port3  
# 相应的运行容器使用的命令  
docker run -p port1 -p port2 -p port3 image  
# 还可以指定需要映射到宿主机器上的某个端口号  
docker run -p host_port1:port1 -p host_port2:port2 -p host_port3:port3 image
```

 端口映射是docker比较重要的一个功能，原因在于我们每次运行容器的时候容器的IP地址不能指定而是在桥接网卡的地址范围内随机生成的。宿主机器的IP地址是固定的，我们可以将容器的端口的映射到宿主机器上的一个端口，免去每次访问容器中的某个服务时都要查看容器的IP的地址。对于一个运行的容器，可以使用docker port加上容器中需要映射的端口和容器的ID来查看该端口号在宿主机器上的映射端口。 

### ENV（用于设置环境变量）

构建指令，在image中设置一个环境变量。格式:

```bash
ENV <key> <value>
```

<src> 是相对被构建的源目录的相对路径，可以是文件或目录的路径，也可以是一个远程的文件URL; source，就是源文件。<dest> 是container中的绝对路径。destination，就是目标文件夹。举个例子，如果src里面是个tar之类的文件，会直接解压缩到dest里面。

### VOLUME（指定挂载点)

设置指令，使容器中的一个目录具有持久化存储数据的功能，该目录可以被容器本身使用，也可以共享给其他容器使用。我们知道容器使用的是AUFS，这种文件系统不能持久化数据，当容器关闭后，所有的更改都会丢失。当容器中的应用有持久化数据的需求时可以在Dockerfile中使用该指令。

人话就是：把一个可以保存更改的文件挂到container上。不保存更改？？？格式:

```bash
VOLUME ["<mountpoint>"]
```

```bash
FROM base  
VOLUME ["/tmp/data"]
```

 /tmp/data目录中的数据在容器关闭后，里面的数据还存在。 

如果另一个容器也有持久化数据的需求，且想使用上面容器共享的/tmp/data目录，那么可以运行下面的命令启动一个容器： 

```bash
docker run -t -i -rm -volumes-from container1 image2 bash
```

 container1为第一个容器的ID，image2为第二个容器运行image的名字。 

### WORKDIR（切换目录）

 设置指令，可以多次切换(相当于cd命令)，对RUN,CMD,ENTRYPOINT生效。格式: 

```bash
WORKDIR /path/to/workdir
```

```bash
# 在 /p1/p2 下执行 vim a.txt  
WORKDIR /p1 WORKDIR p2 RUN vim a.txt
```

### ONBUILD（在子镜像中执行）

```bash
ONBUILD <Dockerfile关键字>
```

## Dockercompose with YAML



