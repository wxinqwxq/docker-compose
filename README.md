# docker-compose

## 如何使用该镜像 ? ##

**本地模式:**

只需将其作为普通命令运行，包含docker-compose.yml文件的目录
与Docker Unix套接字：
```bash
$ docker run -v "$(pwd)":"$(pwd)" \
             -v /var/run/docker.sock:/var/run/docker.sock \
             -e COMPOSE_PROJECT_NAME=$(basename "$(pwd)") \
             --workdir="$(pwd)" \
             -ti --rm \
             dduportal/docker-compose:latest --help
```

**远程模式**

当使用另一个套接字而不是默认的Unix套接字（远程Docker引擎用例）时，
您可以使用DOCKER_HOST环境变量提供docker-compose的路径。
 假定Docker守护进程在10.0.2.15:2375监听TCP连接：
```bash
$ docker run -v "$(pwd)":"$(pwd)" \
             -e DOCKER_HOST=tcp://10.0.2.15:2375 \
             -e COMPOSE_PROJECT_NAME=$(basename "$(pwd)") \
             --workdir="$(pwd)" \
             --rm \
             dduportal/docker-compose:latest up -d
```