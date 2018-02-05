# 环境搭建

本小节介绍Phaser环境搭建相关的知识。

其实Phaser的环境搭建非常简单，只需要将phaser.js或者phaser.min.js通过script引入即可。

我们建议把Phaser的文件通过服务器serve出来进行访问，你可以在本地使用apache、tomcat、nginx或者任何http server都行，甚至有些编辑器比如WebStorm，也是自带这种功能的。

当然，你也可以双击打开你的html文件，但是我们不建议这样做，因为这样做在使用WebGL渲染模式的时候，加载资源是有问题的。

如果你真的没有任何搭建服务器的经验，那么我这里推荐一个最简单的方法，http-server。

## http-server环境搭建教程

http-server是基于nodejs的，所以第一步，我们先安装nodejs，从node的[官网](https://nodejs.org/en/)下载nodejs的安装包进行安装就行。

安装完成之后，在你电脑的终端运行node -v查看一下node版本：

```
$ node -v
v6.9.3

```

如果能够成功输出版本号，说明nodejs已经安装成功，接下来安装http-server，在终端运行 ``` npm install -g http-server ```，npm工具会自动从网上下载http-server的包并安装，安装完成之后，在你的phaser项目目录下执行http-server，就能够将你的phaser项目通过服务器serve出来了：

```
$ http-server
Starting up http-server, serving ./
Available on:
  http://127.0.0.1:8080
  http://169.254.16.42:8080
Hit CTRL-C to stop the server

```

这时候，在浏览器打开 http://127.0.0.1:8080 ，就能看到页面啦。

***

如果看完这一小节还是不会的话，可以去看Phaser小站的[视频教程](https://www.phaser-china.com/tutorial-detail-8.html)中的环境搭建篇，里面详细介绍了两种搭建环境的方法。

Phaser的环境搭建是学习Phaser的第一步，相比于其他游戏引擎下载复杂的IDE来说，实在是极简。

当然，对于新手来说，搭建环境可能也是困难的，但是我相信，如果你认真看了教程和视频，一定会成功。如果还不行，欢迎到Phaser小站QQ群提问。

不管怎样，希望你都不要放弃，如果你总是这样轻言放弃的话，无论多长时间，你都只是在原地踏步。

