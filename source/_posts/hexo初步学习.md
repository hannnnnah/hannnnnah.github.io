title: hexo初步学习
author: 隐藏的NPC
tags:
  - hexo
categories:
  - hexo
date: 2019-07-01 17:05:00
---
参考文档：

1、[hexo中文文档](https://hexo.io/zh-cn/docs/)

2、[https://blog.csdn.net/sinat_37781304/article/details/82729029](https://blog.csdn.net/sinat_37781304/article/details/82729029)

##### hexo部署到github
1、[安装git](https://git-scm.com/download/win)

2、[安装nodejs](https://nodejs.org/en/)

3、用 npm 安装话经常出现卡住而导致无法正常安装，解决办法就是修改 npm 的安装源，这里选择淘宝 NPM 镜像，这是一个完整 npmjs.org 镜像，你可以用此代替官方版本，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。
```
npm config set registry https://registry.npm.taobao.org
```

4、安装hexo
```
npm install -g hexo-cli
```
![安装hexo](/images/install_hexo.png)

5、查看版本信息
```
hexo -v
```
![查看版本信息](/images/version.png)

6、初始化hexo程序
```
hexo init myblog
```
（更新npm/并更换为国内的npm镜像命令：npm install npm -g/
npm install -g cnpm --registry=https://registry.npm.taobao.org）

7、进入myblog文件夹
```
cd myblog
```

8、
```
npm install
```

9、查看文件夹目录
-  node_modules: 依赖包
- scaffolds：生成文章的一些模板
- source：用来存放你的文章
- themes：主题
- _config.yml: 博客的配置文件

![文件夹目录](/images/mulu.png)

10、打开hexo
```
hexo g
hexo server
```

11、创建以用于提交
```
git config --global user.name "yourname"
git config --global user.email "youremail"
```

12、连接公钥
```
ssh-keygen -t rsa -C "email"
```

13、查看是否成功
```
ssh -T git@github.com
```
（You've successfully authenticated, but GitHub does not provide shell access.）

14、将hexo和GitHub关联起来，修改配置文件_config.yml
```
deploy:
  type: （中间有个空格，以下相同）git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
```

15、安装deploy-git部署命令
```
npm install hexo-deployer-git --save
```

16、清除之前生成的东西
```
hexo clean
```

17、生成静态文章
```
hexo generate/hexo g
```

18、部署文章
```
hexo deploy/hexo d
```

19、github中要新建一个仓库用户名+github.io，访问用户名.github.io即可

##### 设置hexo主题
1、[选择hexo主题](https://hexo.io/themes/)，到github上下载主题放到themes文件夹下
2、修改_config.yml里的theme为该文件夹名称


##### 新增菜单栏选项
1、添加新页面：hexo new page "xx"
2、在主题配置文件的menu中加上该页面
3、在zh-CN.yml文件中加上中文意思