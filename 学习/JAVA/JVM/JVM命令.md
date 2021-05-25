# Docker中的JVM

如果JVM运行在了docker中，想要使用JVM命令查看运行中的程序，首先需要进入到docker。

`docker ps`命令查看运行中的容器

![image-20210114161851557](source/docker中的JVM.assets/image-20210114161851557.png)

`docker exec -it <image_name> bash`进入容器

`jps`查看当前容器运行的进程

