# Docker
---
> docker 让部署变成的轻量、可移植、可拓展、更好的愿景隔离也更大的避免了生产环境与测试的不一致行为

## 术语

+ `docker client`：`docker` 的命令行工具 ^43c2c4
+ `docker daemon`：docker 的守护进程，[[Docker#^43c2c4|`docker client`]]通过命令与 `docker daemon`， 做交互。 ^a8aaad
+ `docker host`：宿主机，[[Docker#^a8aaad|docker daemon]] 的运行环境服务器
+ `image`：镜像，可以理解为一个容器的模板，通过一个镜像可以创建多个容器。
+ `container`：最小型的一个操作系统环境，可以对各种服务以及应用容器化，是镜像的实例化
+ `registry`：镜像仓库，储存大量的镜像，可以从镜像仓库拉取和推送
![[Pasted image 20220809153359.png]]
