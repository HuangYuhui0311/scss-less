## Sass安装（windows版） ##

- 在 Windows 平台下安装 Ruby 需要先有 Ruby 安装包，大家可以到 Ruby 的官网（http://rubyinstaller.org/downloads）下载对应需要的 Ruby 版本。
- Ruby 安装文件下载好后，可以按应用软件安装步骤进行安装 Ruby。在安装过程中，个人建议将其安装在 C 盘下，在安装过程中选择第二个选项（不选中，就会出现编译时找不到Ruby环境的情况），如下图所示：![](img/01.png)
- Ruby 安装完成后，在开始菜单中找到新安装的 Ruby，并启动 Ruby 的 Command 控制面板，如下图所示：![](img/02.png)
- 当你的电脑中安装好 Ruby 之后，接下来就可以安装 Sass 了。同样的在windows下安装 Sass 有多种方法。但这几种方法都是非常的简单，只需要在你的命令终端输入一行命令即可。

##1、通过命令安装 Sass ##

打开电脑的命令终端，输入下面的命令：

	gem install sass

提醒一下，在使用 Mac 的同学，可能需要在上面的命令前加上"sudo"，才能正常安装：

	sudo gem install sass

如果上面的方法没有安装成功，可以使用下面的两种方法。

## 2、通过 Compass 来安装 Sass ##

- 除了使用 gem 命令来安装 Sass 之外，还可以通过安装 compass 来安装 Sass，因为 Compass 是基于 Sass 开发的一个框架。也就是说，你安装了 Compass，也就同时安装好了 Sass。

同样的在你的命令终端输入下面的命令：

	sudo gem install sass

执行完上面的命令之后，就开始安装 Compass 和 Sass。

	注：Compass 是一个成熟的、基于 Sass 开发的一个框架，这里面集成了很多写好的 mixins 和 Sass 函数。

## 3、本地安装 Sass ##

由于有时候直接使用上面的命令安装会让你无法正常实现安装（网络受限原因），当碰到这种情况之时，那么安装需要特殊去处理，可以通过下面的方法来实现 Sass 的正常安装：

可以到 Rubygems(http://rubygems.org/) 网站上将 Sass 的安装包（http://rubygems.org/gems/sass）下载下来，然后在命令终端输入：

	gem install <把下载的安装包拖到这里>

直接回车即可安装成功。

	注：在 iOSX 系统平台，可以直接将下载的安装包拖到 "gem install" 后面，如果在是 Windows 系统，需要手功输入安装的文件路径。

## 4、淘宝 RubyGems 镜像安装 Sass ##

除了下载 Sass 安装包到本地安装之外，碰到网络原因无法安装时还可以使用淘宝 RubyGems 镜像安装 Sass。只是我们需要通过 gem sources 命令来配置源，先移除默认的 https://rubygems.org 源，然后添加淘宝的源 https://ruby.taobao.org：

第一步：移动默认的源

	gem sources --remove https://rubygems.org/

第二步：指定淘宝的源

	gem sources -a https://ruby.taobao.org/

第三步：查看指定的源是不是淘宝源

	gem sources -l

返回结果如下：

	*** CURRENT SOURCES ***
	https://ruby.taobao.org

请确保只有 ruby.taobao.org。如果无误之后，执行下面的命令：

	gem install sass

## 查测 Sass ##
	sass -v

## 更新 Sass ##
	gem update sass

## 卸载（删除）Sass ##
	gem uninstall sass
	
<a href="http://www.imooc.com">资源来源：慕课网</a>
