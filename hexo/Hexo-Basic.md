﻿---
title: 使用 Github 空间搭建 Hexo 技术博客
date: 2016-12-11 18:10:07
description: "如何搭建 Hexo 博客、写博客！"
categories: [Hexo]
tags: [Hexo,Git,Github,Node.js]
---


## 部署前介绍 

### Hexo 是什么

- Hexo 的中文官网：<http://hexo.io/zh-cn/>
- 作者 Tommy Chen：<https://zespia.tw/>
- 在我的理解里面：Hexo 是一个基于 Node.js 快速、简洁且高效的博客框架，可以将 Markdown 文件快速的生成静态网页，托管在 GitHub Pages 上。
- 而官网自己是这样说的：

> Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。


### 适合人群

- 只想搭建一个技术博客的人（真心别搞太多，你没那么多精力）


### 搭建所需软件

- 各个软件官网：
    - git：<http://git-scm.com/>
    - node.js：<http://nodejs.org/>


### 文章前提

- 如果你对上面要求的软件一个都不了解的话，建议你先看如下内容（只是让你们先了解下，当时别照着文章内容做）：
    - [如何搭建一个独立博客——简明Github Pages与Hexo教程](http://www.jianshu.com/p/05289a4bc8b2)
    - [通过Hexo在Github上搭建博客教程](http://www.jianshu.com/p/858ecf233db9)
    - [hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)
    - [手把手教你建github技术博客](http://www.jianshu.com/p/701b1095da11)
    - [如何搭建一个独立博客——简明Github Pages与Hexo教程](http://www.jianshu.com/p/05289a4bc8b2)
    - [windows下搭建hexo博客并将其部署到GitCafe终极教程](http://www.jianshu.com/p/e858a90d0a17)
    - [使用Hexo搭建博客（三），博客配置、主题和写作](http://www.jianshu.com/p/db7e64d86067)
    - [Hexo搭建WiKi](http://www.jianshu.com/p/e7413116e9d4)
    - [怎么用hexo上传一个README.md到github?](https://www.zhihu.com/question/28058973)


### 域名绑定

- 如果你一开始就打算要绑定域名，则下面教程中所有可以填写域名的地方你都填写上你要绑定的域名，如果你没独立域名，那就使用 Github 默认给你的：username.github.io 域名即可。


------


## 部署开始

### git 安装

- 双击运行 **Git-2.9.9.1-64-bit.exe**，接下来一律下一步，不需要多余的选择，假设你安装的目录位置跟我一样：C:\Program Files\Git
- 打开 Git Bash（路径：C:\Program Files\Git\git-bash.exe），输入：`git --version`
    - 如下图，如果出现：**git version 2.9.3.windows.1**，这表示安装成功
    - ![验证 git 安装](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/check-git-version.png)


### Node.js 安装

- 双击运行 **node-v6.6.0-x64.msi**，接下来一律下一步，不需要多余的选择。
- 安装完之后，打开 Git Bash，输入：`npm -v`
    - 如下图，如果出现：**3.10.3**，则表示 Node.js 安装成功。如果你没有显示这个信息，我怀疑你需要重启电脑试试看，因为我在给我弟讲解这一步的时候发现有这个问题。
    - ![验证 node.js 安装](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/check-node-npm-version.png)


### Node.js 源设置

- 在安装 Hexo 之前，先说一下 Node.js 的源，Node.js 官方源默认是：<http://registry.npmjs.org>，但是由于在国外，说不定你使用的时候就抽风无法下载任何软件。所以我们决定暂时使用淘宝提供的源，淘宝源官网：<http://npm.taobao.org/>
- 在 Git Bash 中我们执行下面这一句（这是一整句的）：

``` bash
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"
```

- 现在验证下是否可以使用淘宝的 cnpm 命令：`cnpm info express`
    - 如果能输出一大堆介绍，则说明成功了，以后每次要使用淘宝的源都需要这样来。现在除了默认的 **npm**，还多了一个 **cnpm** 可以使用，我们下面有关安装的讲解内容也都是基于此临时命令。
    - 如果输出：bash: cnpm: command not found，则表示没成功，需要你在排查下


### 安装 Hexo 框架

- 安装 Hexo（注意，现在是 cnpm 开头了，不是 npm 了）：`cnpm install -g hexo-cli`
    - 安装时间不一定很快，有可能需要等 3 ~ 5 分钟。
    - 安装完有 WARN 警告也没关系的。


### 创建 Hexo 项目

- 现在假设我要创建一个名为 hexo 的项目，项目目录就放在：D:\Workspace\blog 目录下，所以我们在 D:\Workspace\blog 目录下创建一个 hexo 目录。现在这个项目的全路径是：D:\Workspace\blog\hexo
- 打开 Git Bash：
    - 进入该目录：`cd D:/Workspace/blog/hexo`
    - 然后执行：`hexo init`，这个时间也会比较长，也有可能要等几分钟，有显示 WARN 也不用管
    - 最后执行：`cnpm install`，有显示 WARN 也不用管
    - 安装完成之后，D:\Workspace\blog\hexo 目录结构是这样的：
        - ![安装 hexo 后的目录结构](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/hexo-init-file-catalog.png)
    - 现在我们启动 hexo 本地服务，看下默认的博客是怎样的，命令：`hexo server`
    - 现在用浏览器访问：<http://localhost:4000/>，效果如下图
        - ![默认模板效果](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/hexo-default-theme-home-page.png)
    - 如果要停止 hexo 服务：在 Git Bash 下按 `Ctrl + C` 即可


### 选用其他主题

- 由于默认主题太大众了，所以现在我们换个主题。
- 你可以去这里找主题：
    - hexo-theme：<https://hexo.io/themes/>
    - hexo-github-theme-list：<https://github.com/hexojs/hexo/wiki/Themes>
    - 有那些好看的hexo主题？：<http://www.zhihu.com/question/24422335>
- 我这里选择的 **yelee**：<https://github.com/MOxFIVE/hexo-theme-yelee>
    - 原因是能最大化衬托出：目录、文章内容、代码块。因为我对这个博客的定位就是用来放技术类内容，所以不会让它太杂或是太花。只是目前这个颜色偏浅，后续还需要调整。
- 现在假设你跟我要用的模板是一样：
    - 还是让 Git Bash 保持在 D:\Workspace\blog\hexo 目录下，然后输入命令：`git clone https://github.com/MOxFIVE/hexo-theme-yelee.git themes/yelee`
    - 这样就在 D:\Workspace\blog\hexo\themes 目录下生成了一个 yelle 文件夹，里面有我们刚刚 clone 下来的主题内容。
    - 如果以后你不自己修改这个主题的话，可以考虑经常更新下作者的更新内容：
        - `cd D:/Workspace/blog/hexo/themes/yelee`
        - `git pull origin master`
- 下载好主题文件之后，我们现在要修改 D:\Workspace\blog\hexo 目录下的项目配置文件：**\_config.yml**，把对应的主题目录名改下，编辑如下图。
    - ![修改主题目录](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/hexo-modify-theme.png)
- 更改主题目录名后，我们还要重新生成主题静态内容：
    - 继续在 Git Bash 中输入命令：
        - 重新生成静态博客的所有内容：`hexo generate`
        - 重启 hexo 本地服务：`hexo server`
        - 重新访问：<http://localhost:4000/>，效果如下图
        - ![新主题效果](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/hexo-yalee-theme-home-page.png)


### 创建 Github pages 并 SSH 授权

- 现在假设你已经有一个 Gtihub 账号，你还需要一个特别的仓库，特别在仓库名就是你的 Github 账号登录名，比如我的用户名是：andyadc，那我要创建的仓库名字完整滴填写是：andyadc.github.io，具体效果如下图。
    - ![创建 github pages](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/create-gitpages-repository.png)
- 创建好仓库之后，要本地生成 SSH 秘钥，方便电脑上的 git 软件好提交内容到 Github 上
    - 在 Git Bash 中，输入：`ssh-keygen -t rsa -C "你的邮箱地址"`，然后回车，回车，再回车，一共 3 次回车，具体含义自己 Google。
    - 比如我的：`ssh-keygen -t rsa -C "andaicheng@gmail.com"`，生成后效果如下图：
    - ![生成 ssh 密钥](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/ssh-keygen.png)
    - 此时，生成密钥后，在你电脑目录：C:\Users\你的计算机用户名\\.ssh 下，会生成两个文件：
        - 私钥：**id_rsa**
        - 公钥：**id_rsa.pub**
        - 如果生成的不是这样的文件，那删除掉这两个生成的，重新执行上面的命令，让它再一次生成。
    - 现在用记事本打开 id_rsa.pub，复制文件中的所有内容。
        - 访问：<https://github.com/settings/ssh>，添加新秘钥，效果如下图
            - Title：自己随便取
            - Key：把刚刚复制的都粘贴进来
            - ![添加密钥](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/github-add-ssh-keys.png)


### 把本地的博客内容同步到 Github 上

- 要把本地的静态博客同步到 Github，我们还需要先安装两个跟部署相关的 hexo 插件：
    - 继续在 Git Bash 中输入：
    - `cnpm install hexo -server --save`
    - `cnpm install hexo-deployer-git --save`
- 编辑全局 hexo 的配置文件：**\_config.yml**
    - 官网对此配置的介绍：<https://hexo.io/zh-cn/docs/configuration.html>
    - 我自己的编辑内容初稿（你需要认真看的是含有中文注释的内容）：
    
``` bash
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site，这一块区域主要是设置博客的主要说明，需要注意的是：每个冒号后面都是有一个空格，然后再书写自己的内容的
title: Andy Code
subtitle: Andy's Blog
description: xxxx
author: Andy An
email: andaicheng@gmail.com
language: zh-CN
timezone:

# URL，这一块一般可以设置的是 url 这个参数，比如我要设置绑定域名的，这里就需要填写我的域名信息
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://blog.andyadc.com
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  auto_detect: false
  tab_replace:

# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: yelee

# Deployment
## 这里是重点，这里是修改发布地址，因为我们前面已经加了 SSH 密钥信息在 Github 设置里面了，所以只要我们电脑里面持有那两个密钥文件就可以无需密码地跟 Github 做同步。
## 需要注意的是这里的 repo 采用的是 ssh 的地址，而不是 https 的。分支我们默认采用 master 分支，以后你翅膀硬了要换其他也无所谓。
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:andyadc/andyadc.github.io.git
  branch: master
  
```

- 编辑全局配置后我们需要重新部署：
    - 继续在 Git Bash 中输入命令：
    - 先清除掉已经生成的旧文件：`hexo clean`
    - 再生成一次静态文件：`hexo generate`
    - 在本地预览下：`hexo server`
    - 本地没问题之后，Ctrl + C 停掉本地预览。
    - 在部署到 Github 之前，需要先确定你是否已经用过 Git，如果你没用过，则此时你需要做如下设置，在 Git Bash 中依次输入下面两个命令：
        - `git config --global user.email "你的 Github 注册邮箱地址"`
        - `git config --global user.name "你的 Github 用户名"`
    - 使用部署命令部署到 Github 上：`hexo deploy`，有弹出下面提示框，请输入：`yes`
        - ![确认提交](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/hexo-git-deploy-confirm.png)
    - 提交成功效果如下：
        - ![提交成功](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/hexo-git-deploy-success.png)
    - 访问服务器地址进行检查：<http://andyadc.github.io>，效果如下
        - ![服务器效果](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/hexo-server-preview.png)
    - 但是，也不排除你 deploy 不了到 Github，报这个错误：`Host key verification failed`，那解决办法如下：
        - 还是在 Git Bash 界面中，输入如下命令：`ssh -T git@github.com`，根据界面提示，输入：`yes` 回车。之后你可以再试一下是否可以 deploy。
- 通过上面几次流程我们也就可以总结：以后，每次发表新文章要部署都按这样的流程来：
    - `hexo clean`
    - `hexo generate`
    - `hexo deploy`
- 也因为这几个命令太频繁了，所以又有了精简版的命令：
    - `hexo clean == hexo clean`
    - `hexo g == hexo generate`
    - `hexo s == hexo server`
    - `hexo d == hexo deploy`


### 绑定域名

- 绑定域名不排除会遇到很多网络问题或是七七八八，所以这里先提供先官网的一些说明：
    - <https://help.github.com/articles/setting-up-your-pages-site-repository/>
    - <https://help.github.com/articles/quick-start-setting-up-a-custom-domain/>
    - <https://help.github.com/articles/setting-up-an-apex-domain/>
    - <https://help.github.com/articles/troubleshooting-custom-domains/>
    - <https://help.github.com/articles/custom-domain-redirects-for-github-pages-sites/>
- 首先我们要一个 CNAME 文件（文件名叫 CNAME，没有文件后缀的），把该文件放在 D:\Workspace\blog\hexo\source 目录下，以后一些需要放在根目录的资源文件都可以放这里。如果你找不到这样的文件可以到我的项目上下载：<https://github.com/andyadc/andyadc.github.io>
    - CNAME 上的内容需要写你具体要绑定的域名信息，比如我是：**blog.andyadc.com**，具体你可以参考下图：
        - ![设置 CNAME 文件](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/add-cname.png)
- 接着我们需要到 阿里云 上设置域名解析
    - ![设置域名解析](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/github-pages-domain-resolution.png)
    
- 设置好之后，等过几分钟域名解析好之后，我们访问：<http://blog.andyadc.com>，效果如下：    
    - ![域名访问效果](http://andyadc-image.oss-cn-shanghai.aliyuncs.com/blog-hexo-image/domain-resolution-success.png)
	- Github 提示，建议我们使用 CNAME 方式来指向，别用 IP，所以建议你这样配置，还是以我的为例：
		- 主机记录：blog
		- 记录类型：CNAME
		- 记录值：andyadc.github.io.（后面的这个点别忘记了）
		- 还有，要记得把 CNAME 那个文件再 deploy 到 Github 哦，不然还是访问不了的。

### Hexo 新文章内容的开头


- hexo 新文章内容的开头需要这样定义：
    - categories：表示文章所属分类
    - tags：表示文章所属标签

``` bash
---
title: 这是文章标题
date: 2016-12-11 17:58:27
categories: [Hexo,IntelliJ IDEA]
tags: [Hexo,IntelliJ IDEA,Git,Github,Node.js]
---
```

<!-- more -->
## 主题优化 

### 主题配置介绍 

我这里只讲自己在使用的 yelle 主题，你可以参考下，可能还有一些改动我后续会自己在慢慢改，但是大体基本也就这样了。

从中我们也可以看出，对于主题来讲，大部分可以配置的地方其实都是在这里的，所以对于主题的使用者来讲，懂这里很重要。

- 基本上主题的配置文件都是有内容改，但是下面这几点我觉得特别重要：
- `duoshuo`，如果你是打算采用多说评论系统的话，你需要设置这里
- `youyan`，有言也是国内实用比较多的评论系统之一，个人感觉相对比较稳定
- `open_in_new`，我个人觉得这个东西就应该是 true，不是用新标签的都是坏人
- `baidu_tongji`，我个人使用的是百度统计，具体百度统计的使用可以查看百度统计官网：<http://tongji.baidu.com>


### 我的 yelle 主题配置 

``` bash
# >>> Basic Setup | 基础设置 <<<

# Header | 主菜单
## About Page: `hexo new page about`
## Tags Cloud Page: `hexo new page tags`
menu:
  主页: /
  关于我: /about/
  标签云: /tags/
  所有文章: /archives/
  IntelliJ IDEA: /tags/IntelliJ IDEA

# Link to your avatar | 填写头像地址
avatar: /img/avatar.png

# Small icon of Your site | 站点小图标地址
favicon: /favicon.png

# If your site' url is 'http://yoursite.com/blog', set root_url as '/blog/'
# 网站若存放在子目录，请按上面格式填写
# https://hexo.io/docs/configuration.html#URL
root_url: 

# Social info. Bar | 社交信息展示
## Keep "mailto:" in Email | 设置 Email 时保留 "mailto:"
## Encrypt email 加密邮件地址 http://ctrlq.org/encode/
## RSS requires a plugin to take effect | 使用 RSS 需先安装对应插件
## https://github.com/hexojs/hexo-generator-feed

subnav:
  Email: "mailto:andaicheng@gmail.com"
  #新浪微博: "sina weibo"
  GitHub: "https://github.com/andyadc"
  RSS: "/atom.xml"
  #V2EX: "#"
  #知乎: "zhihu"
  #豆瓣: "douban"
  #简书: "jianshu"
  #SegmentFault: ""
  #网易云音乐: "netease"
  #虾米音乐: "xiami"
  #Facebook: "#"
  #Google: "#"
  #Twitter: "#"
  #LinkedIn: "#"
  #QQ: "#"
  #微信: "Wechat"
  #PayPal: "#"
  #StackOverflow: "#"
  #Instagram: "#"
  #Flickr: "#"
  #reddit: ""
  #Medium: ""
  #TiddlyWiki: ""
  #Tumblr: ""
  #_500px: ""

# >>> Conments 评论系统 <<<
# Chose ONE as your comment system and keep others disable.
# 选一个作为网站评论系统，其他保持禁用。

disqus: 
  #on: true
  shortname: 
  # https://help.disqus.com/customer/en/portal/articles/466208-what-s-a-shortname-
  # It is unnecessary to enable disqus here if 
  # you have set "disqus_shortname" in your site's "_config.yml" 

duoshuo: 
  #on: true
  domain: 
  # 是否开启多说评论，http://duoshuo.com/create-site/
  # 使用上面网址登陆你的多说，然后创建站点，在 domain 中填入你设定的域名前半部分
  # http://<要填的部分>.duoshuo.com (domain只填上<>里的内容，不要填整个网址)

youyan:
  on: true
  id: 1738968
  # 是否开启友言评论，http://www.uyan.cc/index.php
  # id 中填写你的友言用户数字ID，注册后进入后台管理即可查看
  # 友言服务在 Web 环境下运行，普通本地环境无法查看，请部署后在线上测试。


# >>> Style Customisation 样式自定义 <<<

# Background | 背景
## "5": show images form bg-1.jpg to bg-5.jpg in `/yelee/source/background/`
## "5": 显示`/yelee/source/background/`文件夹中 bg-1.jpg 到 bg-5.jpg 这5张图片
## "0": white-gray background | 淳朴灰白背景
background_image: 0

highlight_style:
  on: true
  inline_code: 3  # Value: 0 - 9 可选，3还不错
  code_block: 2  # Value: 0 - 4 
  # Set inline_code to style highlight text
  # Chose a highlight theme for code block
  # 通过 inline_code 切换内置文本高亮样式
  # 通过 code_block 切换内置代码高亮配色主题

blockquote_style:
  on: true
  blockquote: 3  # Value: 0 - 7 可选
  # 自定义文章「引用部分」的样式

# 左边栏宽度 px
left_col_width: 330

# Copyright info. of post | 文末版权信息
copyright: true

# Table of contents | 文章目录
toc: true

# 目录中标题不换行
# Keep TOC title on the same line | 
toc_nowrap: true

# 自定义"阅读全文"链接按钮的显示文字
# Customize the text on excerpt link
excerpt_link: more

# 是否显示边栏中的搜索框（仅样式，未添加搜索功能）
# Search Box in left column
search_box: false

# 是否开启主页及加载头像时的动画效果
# Animation in Homepage and Loading avatar
animate: true

# Load jQuery UI to style tooltips
# 工具提示框样式美化
jquery_ui: false

# >>> Small features | 小功能设置 <<<

# 是否开启边栏多标签切换
# Birdhouse button in left column
tagcloud: true

# Blogroll, Link exchange | 友情链接
friends:
  GitHub: https://github.com/
  IntelliJ IDEA: http://www.jetbrains.com/idea/
#friends: false

#是否开启“关于我”。
aboutme: 此地只专注于技术
#aboutme: true

# 是否在新窗口打开链接
# Open ALL link in a new tab
open_in_new: true

# Customize feed link 自定义订阅地址
rss: /atom.xml


# >>> Vendors | 第三方工具 & 服务 <<<

# images viewer | 图片浏览器
## http://www.fancyapps.com/fancybox/
fancybox: true

# Display Math(LaTeX, MathML...) | 数学公式支持
## https://www.mathjax.org/
mathjax: false

# Socail Share | 是否开启分享
share: true

# 百度、谷歌站长验证。填写 HTML 标签 content
# Site Verification for Google and Baidu. HTML label content.
baidu_site: 
google_site: 

# Fill in Google Analytics tracking ID, #e.g. UA-XXXXX-X
google_analytics: 

# 百度统计 http://sitecenter.baidu.com/sc-web/
# 查看代码，填入 //hm.baidu.com/hm.js? 之后的内容
baidu_tongji: b68dade9d355a0b3d875d0ffbbe1f212

# 不蒜子网站计数设置
# http://ibruce.info/2015/04/04/busuanzi/
visit_counter:
  on: true
  site_visit: 本站到访数
  page_visit: 本页阅读量

# GitHub Repo Widget
# https://github.com/hustcc/GitHub-Repo-Widget.js
github_widget: false
```

## 常用页面添加

### 404、关于我、标签页

- 还是以上一篇文章我们讲解的项目根目录上：E:\git_work_space\hexo，在该目录启动 Git Bash：
- 新增一个 404 页面：`hexo new page 404`
- 新增一个 about 页面：`hexo new page about`
- 新增一个 tag 标签云页面：`hexo new page tags`
- 新增一个 robot.txt 文件，把该文件放在：E:\git_work_space\hexo\source 目录下，如果你没有该文件可以到我的项目上找：<https://github.com/judasn/judasn.github.io>
- robot 文件内容：

``` bash
User-Agent: *
Allow: /
Disallow: /background
Disallow: /css
Disallow: /fancybox
Disallow: /font-awesome
Disallow: /img
Disallow: /js
Sitemap: http://code.youmeek.com/sitemap.xml
Sitemap: http://code.youmeek.com/baidusitemap.xml
```


### 置顶文章方法

- 参考：[解决Hexo置顶问题](http://www.netcan666.com/2015/11/22/%E8%A7%A3%E5%86%B3Hexo%E7%BD%AE%E9%A1%B6%E9%97%AE%E9%A2%98/)
- 编辑这个文件：`node_modules/hexo-generator-index/lib/generator.js`
- 覆盖原文件内容，采用下面内容：

``` bash
'use strict';

var pagination = require('hexo-pagination');

module.exports = function(locals){
  var config = this.config;
  var posts = locals.posts;

    posts.data = posts.data.sort(function(a, b) {
        if(a.top && b.top) { // 两篇文章top都有定义
            if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
            else return b.top - a.top; // 否则按照top值降序排
        }
        else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
            return -1;
        }
        else if(!a.top && b.top) {
            return 1;
        }
        else return b.date - a.date; // 都没定义按照文章日期降序排

    });

  var paginationDir = config.pagination_dir || 'page';

  return pagination('', posts, {
    perPage: config.index_generator.per_page,
    layout: ['index', 'archive'],
    format: paginationDir + '/%d/',
    data: {
      __index: true
    }
  });
};
```

- 然后在文章头部的：Front-matter 位置加上一个：`top: 1000` 的内容。数值越大，越靠前


## 添加一些不希望被渲染的文件到 hexo

- 因为我们使用的是 Github 项目做空间，所以一般项目我们都要放一个 README.md 文件，而我们希望这个文件不被 hexo 渲染成 HTML 文件，我们需要这样做：
  - 把 README.md 放在这个目录下：`hexo\source\README.md`
  - 编辑这个配置文件：`hexo\_config.yml`，找到这个关键字：`skip_render`，然后这样写：
  ``` nginx
  skip_render: 
      - README.md
  ```
- 有时候我们需要排除一整个目录，道理跟上面一样，比如你现在访问：<http://code.YouMeek.com/i>，你发现会跑到我的一个备份导航中，而我是通过这样配置来实现的：
  - 这里的 `i` 是我的目录名称，因为我的真正导航地址是：<http://i.YouMeek.com>，所以取这样的目录名字方便记忆。
  - 而 `i/**` 这里的后缀的两个星号表示这个目录下包括子目录，其所有文件都被忽略渲染。
  - 对于一些 HTML 和 CSS、JS 这类也要注意，hexo 有一套自己的渲染方式，比如可能会对你的 JS 做一些特殊处理，所以可能会让你的 JS 失效，所以最好按我这种方式来排除掉。
  ``` nginx
  skip_render: 
    - README.md
    - i/**
  ```


## 插件推荐

### 插件的基本使用命令

- 插件官网：<https://hexo.io/plugins/>
- 安装插件：`npm install 插件名 --save`
- 卸载插件：`npm uninstall 插件名`
- 更新插件和博客框架（需要在 E:\git_work_space\hexo 目录下）：`npm update`
    - 它实质上是通过项目根目录下 package.json 文件更新各大组件

### 必备插件

- 支持RSS：`npm install hexo-generator-feed --save`
- 生成站点地图：`npm install hexo-generator-sitemap --save`
- 生成百度站点地图：`npm install hexo-generator-baidu-sitemap --save`
- HTML 压缩：`npm install hexo-html-minifier --save`
- JavaScript 压缩：`npm install hexo-uglify --save`
- CSS 压缩插件：`npm install hexo-clean-css --save`
- SEO优化：`npm install hexo-generator-seo-friendly-sitemap --save`
- 搜索支持，需要主题有对应的设置：`npm install hexo-generator-search --save`
