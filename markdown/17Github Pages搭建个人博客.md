# Github Pages搭建个人博客

## Github Pages搭建个人博客

### 参考资料

- 搭建博客

	- https://www.cnblogs.com/orchidbaby/p/7686136.html

	- https://zhuanlan.zhihu.com/p/25729240

	- https://zhuanlan.zhihu.com/p/28321740

	- https://www.jianshu.com/p/efebead840b2

- 了解更多

	- Github Pages

		- https://pages.github.com/

	- GitHub Desktop

		- https://desktop.github.com/

	- 两大主流的静态博客框架

		- jekyll

			- 官网

				- https://www.jekyll.com.cn/

			- 主题下载地址

				- https://jamstackthemes.dev/
				- http://jekyllthemes.org/

				- https://jekyllthemes.io

		- hexo

			- 需先安装node.js

				- https://nodejs.org/en/

			- 需先安装Git

				- https://git-scm.com/

			- 安装hexo

				- 官网

					- https://hexo.io/
					- https://hexo.io/zh-cn/docs/

				- github

					- https://github.com/hexojs

			- 主题下载地址

				- https://github.com/hexojs/hexo/wiki/Themes

				- https://hexo.io/themes/

			- 别人的优秀博客示例

				- https://oysz2016.github.io/
				- https://joeybling.github.io

		- 其他主题下载

			- https://html5up.net/

### 搭建步骤

- 第一步：通过Github Pages搭建一个简单的个人博客

	- 1）登录Github，新建一个仓库(仓库名格式必须是：github用户名.github.io)

	- 2）发布Github Pages

		- 进入Settings

		- 找到GitHub Pages，选择Source下的分支"main"，并点击Save保存。

			- 这里顺便提一点，受美国“Black Lives Matter”运动影响，Github替换掉了master等敏感术语，自2020.10.1日起，Github上的默认主分支更名为"main"。
		- 保save成功就自动发布Github Pages site，可直接访问该网站，如图示

		- 你还可以点击Choose a theme，选择一个"Jekyll"的主题。

			- 选择主题后，刷新网站

- 第二步：使用jekyll或hexo框架更换博客主题

	- 上面，我们已经成功搭建了一个简单的个人博客网站。在这里，推荐两大主流的静态博客框架Jekyll和Hexo，优化我们的博客界面，根据个人喜好，个人更偏向于Hexo。其中，Jekyll是基于Ruby语言编写，Hexo是node.js编写，在性能和速度上Hexo更好一些。
	- 不管是Jekyll还是Hexo，更换主题的方式都有两种：

		- 1）非命令的方式，直接将主题下载下来然后推送到github上。
		- 2）命令的方式，使用Jekyll命令或Hexo命令生成静态页面、提交代码到github上(这种方式需要安装相关的软件)。

	- （方式一）更换jekyll主题(非Jekyll命令)

		- Jekyll主题下载地址

			- https://jamstackthemes.dev/
			- http://jekyllthemes.org/
			- https://jekyllthemes.io

		- 步骤：

			- 1）下载jekyll的主题zip包并解压。

				- 访问http://jekyllthemes.org/，选择主题点击Download下载zip包并解压。

			- 2）安装GitHub Desktop。(非必须，GitHub Desktop可方便将本地代码提交到Github，如果你习惯用Git命令提交代码就可以不安装)

				- 官网https://desktop.github.com/，下载后直接双击GitHubDesktopSetup.exe进行安装。

				- 安装成功后登陆关联Github账号。

			- 3）下载Github代码到本地、替换为jekyll主题的内容、提交修改后的代码到Github上。(这里演示用Github Desktop下载和提交代码，你亦可直接使用Git命令执行操作)

				- 通过Github Desktop将Github代码下载本地。

					- 点击Clone a repository...

					- 选择要远程Github代码及保存路径，点击Clone将代码下载到本地。

					- 下载成功如图示：

				- 删除lyf524951805.github.io项目下除.git外的所有文件，并加Jekyll主题的代码复制到该目录下。

				- 打开Github Desktop，提交本地修改后的代码到远程Github上。

					- 先提交到本地仓库

					- 再push到远程仓库

					- 推送成功如图示，我们看到Github代码。

					- 至此，Jykell主题替换成功，我们重新访问个人博客。

	- （方式二）更换Hexo主题(Hexo命令)

		- 跟Jekyll替换主题的方式一样，我们可先将主题代码下载到本地，然后替换本地代码并将新代码提交到Github上来完成Hexo主题的替换。下面演示替换Hexo主题的另一种方式：通过Hexo命令。
		- Hexo主题下载地址

			- https://github.com/hexojs/hexo/wiki/Themes

			- https://hexo.io/themes/

		- 步骤：

			- 1）软件安装(使用hexo命令需要安装相关软件)

				- 1）安装node.js

					- 登录官网https://nodejs.org/en/下载安装包，双击进行安装，一直点击next即可。

					- 安装成功后，执行node -v命令可查看版本信息。

				- 2）安装Git(如果之前已安装过就无需重复安装)

					- 官网https://git-scm.com/，下载后直接双击Git-2.26.2-64-bit.exe即可安装。

					- 安装成功后，执行git --version命令查看版本信息。

				- 3）安装Hexo(node.js和Git安装完后，就可安装Hexo)。

					- 执行命令安装Hexo：npm install -g hexo-cli

					- 顺便安装hexo-deployer-git，方便我们直接使用hexo deploy命令将代码推送到Github上：npm install hexo-deployer-git --save

						- 如果不安装hexo-deployer-git，使用hexo deploy命令时会报错：hexo deploy报错ERROR Deployer not found: git

			- 2）使用hexo命令制作网站

				- hexo常用命令(官网https://hexo.bootcss.com/docs/commands.html)

				- 简单流程描述

					- 1）建站：hexo init <folder>

						- 新建文件夹格式：

						- 示例：hexo init blog

					- 2）下载hexo主题到themes目录下：git clone "主题github地址" themes/主题名

						- 主题下载地址：https://github.com/hexojs/hexo/wiki/Themes
						- 示例：

							- git clone git@github.com:JoeyBling/hexo-theme-yilia-plus.git themes/hexo-theme-yilia-plus

								- 由于内容比较多，clone可能需要一点时间，请耐心等待。clone成功如图：

					- 3）修改_config.yml中的theme字段来指定新主题，并重新生成静态文件。

						- 修改_config.yml文件：

						- hexo clean
						- hexo generate

					- 4）将静态文件推送到github仓库

						- 修改_config.yml文件，配置部署：

						- hexo deploy

				- 步骤细节

					- 新建一个blog网站(可能有点慢，请耐心等待)：hexo init blog

						- 初始化hexo后，多了一个blog目录，如图：

						- 初始化hexo后，自带一篇helloworld的文章(在\source\_posts目录下，是以.md结尾的markdown文件)

					- 将.md格式文章generate成静态文件，并启动本地hexo服务器查看页面效果。

						- 清空缓存文件(清空/blog/public)：git clean

						- 将\source\_posts下的.md文章生成静态页面(到blog/public目录下)：hexo generate

							- 成功后，在blog/下多了一个public目录，保存生成的静态页面代码。

						- 本地启动hexo服务器，并查看网页效果。

							- hexo server

							- 访问http://localhost:4000/

					- 新建一篇文章，并修改blog/_config.yml配置文件，然后将代码提交到Github上。

						- 新建一篇文章

							- 命令：hexo new "第一篇测试文章"

							- 上面的命令会在blog\source\_posts目录下新增一个"第一篇测试文章.md"文件，你也可以不使用hexo new命令手动在该目录下添加.md文件，两者效果一致。
							- 打开并编辑文章内容(Markdown语法)

						- 修改_config.yml配置

							- 1）修改网站的相关信息

								- 修改标题、副标题、描述、语言、时区等信息，修改博客路径。
									- to

							- 2）配置部署信息

								- type为git表示Github类型，repo指定代码仓库的路径，branch表示分支。
									- to

						- 重新生成静态文件

							- hexo clean
							- hexo g

						- 本地启动服务查看页面效果

							- hexo s
							- http://localhost:4000

						- 将public的代码推送到github上

							- 为了避免每次将代码推送到Github上都要手动输入Github的用户名和密码，我们在本地添加公钥，并绑定Github账号。

								- 本地生成公钥，命令：ssh-keygen -t rsa -C "Github的注册邮箱地址"

									- 点Enter，输入y，点Enter，点Enter。
								- 公钥生成成功，如图示：

								- 配置.ssh/id_rsa.pub中的公钥到Github上

									- Github公钥添加成功，如图：

							- 执行命令将blog\public目录中的内容推送到github上：hexo deploy或hexo d

								- 注意：执行hexo deploy命令之前确保已经安装hexo-deployer-git，否则报错：

									- 安装hexo-deployer-git命令：npm install hexo-deployer-git --save

								- 成功部署到Github如图所示：

									- Github代码成功更新，个人博客页面已更新。

					- 下载自己想要的hexo主题并替换

						- blog下有个themes目录，是主题的存储目录，默认有个landscape主题。

							- blog/_config.yml中默认配置的是landscape主题。

						- 因此，我们可以下载更多的主题到themes目录下，然后更改_config.yml中的theme字段来更换主题。
						- 下面演示从https://github.com/hexojs/hexo/wiki/Themes上下载一个自己中意的hexo主题，并进行替换。
						- 步骤

							- 1）选择自己喜欢的主题，点击进入。并拷贝项目的git地址。

							- 2）将代码拷贝到themes目录下

								- clone前先修改postBuffer的大小(设为500MB)：git config --global http.postBuffer 524288000

									- 否则可能报错：

										- error: RPC failed; curl 18 transfer closed with outstanding read data remaining
										- https://blog.csdn.net/dzhongjie/article/details/81152983

								- git clone git@github.com:JoeyBling/hexo-theme-yilia-plus.git themes/hexo-theme-yilia-plus

									- 由于内容比较多，clone可能需要一点时间，请耐心等待。
									- clone成功如图：

								- 修改hexo-theme-yilia-plus主题配置

									- 1）修改\hexo-theme-yilia-plus\_config.yml中的个人配置信息
									- 2）更换\hexo-theme-yilia-plus\source\img中的个人图片

							- 3）修改_config.yml中的theme字段来指定新主题，并重新生成静态文件。

								- hexo clean
								- hexo g
								- 启动本地服务并查看页面效果

									- hexo s
									- 访问http://localhost:4000，无法加载头像，浏览器按F12进入Debug模式，可见缺少/img/head.jpg图片。

									- 添加缺少的图片

										- (方式一)于是添在blog\public\img下添加自己的头像图片，并刷新网页头像加载成功，如图：

										- (方式二)或者将图片添加到主题的\source\img目录下，然后重新hexo clean、hexo g、hexo s，效果一样。

							- 4）效果还满意，最后一步，将blog\public代码推送到Github上。

								- hexo deploy
								- 查看最终效果

