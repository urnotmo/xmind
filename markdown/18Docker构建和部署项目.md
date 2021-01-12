# Docker构建和部署项目

## Docker部署Python项目

### 学习资料

- https://www.runoob.com/docker/docker-tutorial.html

	- 安装

		- https://www.runoob.com/docker/windows-docker-install.html

	- 部署

		- https://www.cnblogs.com/baiboy/p/11014706.html

	- 命令大全

		- https://www.runoob.com/docker/docker-command-manual.html

	- Dockfile编写

		- https://www.runoob.com/docker/docker-dockerfile.html

### 简介

- Docker镜像仓库：https://hub.docker.com/
- Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的镜像中，然后发布到任何流行的 Linux或Windows 机器上，也可以实现虚拟化。
- 在Docker出现之前，软件行业的运维存在着以下这些痛点：

	- 软件的发布和部署低效又繁琐，而且总是需要人工介入。
	- 环境的一致性难移保证。
	- 在不同环境之间迁移的成本较高。

- Docker的应用场景：

	- Web 应用的自动化打包和发布
	- 自动化测试和持续集成、发布
	- 在服务型环境中部署和调整数据库或其他的后台应用

- Docker的优点：

	- 1、快速，一致地交付您的应用程序：持续集成和持续交付（CI / CD）。
	- 2、响应式部署和扩展：轻量级、可移植。
	- 3、在同一硬件上运行更多工作负载：一台机器可以启动N多个容器。

- Docker三大概念

	- 镜像

		- 简单理解：包括项目及和项目所需环境的一个压缩包。

	- 仓库

		- 简单理解：存放镜像的地方，镜像仓库Docker hub与Github类似，Github是存放代码，Docker hub是存放镜像。

	- 容器

		- 简单理解：小型虚拟机，你的代码和环境会被放到这里面。

### 安装

- nice，现在windows上可以直接安装Docker，福音福音!
- https://www.runoob.com/docker/windows-docker-install.html

- 现在 Docker 有专门的 Win10 专业版系统的安装包，需要开启 Hyper-V。
- 配置国内镜像加速器

	- 国内从 Docker Hub 拉取镜像有时会遇到困难，此时可以配置国内镜像加速器。Docker 官方和国内很多云服务商都提供了国内加速器服务，例如：
	- Docker 官方提供的中国 registry mirror：https://registry.docker-cn.com
	- 七牛云加速器：https://reg-mirror.qiniu.com/

### Docker命令大全

- https://www.runoob.com/docker/docker-command-manual.html

- 命令很简单，不用去死记，所有命令看一遍我们大致了解下Docke有哪些操作即可。等我们需要执行某些操作的时候，再去查看具体的命令细节。
- 下面我们就来演示下，如何使用Docker的这些命令来构建和部署一个项目。

### 流程

- 1.本地新建一个Python测试项目helloworld.py

- 2.添加requirements.txt，指定项目需要安装的一些依赖包

- 3.编写Dockerfile文件

	- 这里是直接将代码拷贝到容器中。若你想将整个项目代码打成tar包，然后将这个tar包拷贝到容器中，再执行解压操作也是可以的。

	- 将项目构建成镜像的重点是Dockerfile文件的编写，更多参考：

		- https://www.runoob.com/docker/docker-dockerfile.html

- 4.将项目打成镜像包

	- docker build -f Dockerfile路径 -t 镜像名:标签 .

		- 镜像构建成功如图所示

- 5.大功告成，我们已经成功构建Python项目的镜像。

	- 你可以将镜像包推送到Docker Hub上(类似Github)，等需要的时候再从镜像仓库上拉取下来。
	- 你也可以用docker save命令将镜像打成tar包保存，需要的时候时候docker load命令还原成镜像。

- 6.启动容器(项目)

	- docker run --name lyf-helloworld -d -p 5000:5000 helloworld:liyunfei

		- 启动成功如图

		- 浏览器访问项目成功，如图

- Docker可支持各种操作，这边随便演示下Docker的两个常用命令：

	- 1）进入容器

		- docker exec -it 镜像ID bash

	- 2）替换/拷贝本地文件到容器中

		- docker cp helloworld.py 47eaaf6e8baf:/app/helloworld.py

			- 先查看容器中的原代码

			- 修改本地helloworld.py，添加study()方法

			- 替换成功，容器中的新代码

			- 然后，重新启动容器

				- docker restart 47eaaf6e8baf
				- 浏览器访问修改后的代码成功

