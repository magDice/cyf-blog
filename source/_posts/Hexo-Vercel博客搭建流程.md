---
title: Hexo + Vercel博客搭建流程
date: 2025-09-20 19:15:03
categories: 博客
tags: [Hexo, Vercel, 博客]
---
最近通过`Hexo`和`Vercel`尝试搭建了个人博客，在这里记录一下搭建流程。
在开始之前，需要做好准备工作，官网下载并安装`Node.js`与`git`。
# 1.Hexo本地部署
首先通过以下命令从淘宝`npm`镜像源安装`cnpm`工具：
``` bash
$ npm install -g cnpm --registry=https://registry.npmmirror.com
```
通过`cnpm`可以快速安装`Hexo Cli`：
``` bash
$ cnpm install -g hexo-cli
```
打开`git bash`，初始化一个目录用于存放博客：
``` bash
$ hexo init cyf-blog
```
![初始化](Snipaste_2025-09-20_19-16-14.png)
进入博客目录，下载依赖：
``` bash
$ cd cyf-blog
$ cnpm install
```
接下来可以执行以下命令查看本地部署是否成功：
``` bash
$ hexo clean && hexo g && hexo s
```
![本地部署](Snipaste_2025-09-20_21-24-54.png)
复制链接到浏览器中打开，出现以下页面表示本地部署成功：
![博客页面](Snipaste_2025-09-20_21-21-47.png)

`Hexo`的官网上有很多主题可以帮助我们打造个性化的主页，这里我选择了`next`主题。
首先在项目根目录下创建`git`仓库：
``` bash
$ git init
```
`next`主题的`GitHub`页面上提供了两种安装方式，建议选择直接`install`的方式，这样后面不容易出错：
``` bash
$ npm install hexo-theme-next
```
`Hexo`推荐我们使用备用主题配置，这样在升级主题时配置文件不会被覆盖。
复制主题配置文件到主目录：
``` bash
$ cp node_modules/hexo-theme-next/_config.yml _config.next.yml
```
在博客项目主目录下找到`_config.yml`并打开，将其中`theme`项修改为`next`。
![配置文件](Snipaste_2025-09-20_21-40-35.png)
打开`_config.next.yml`修改方案为`Gemini`，并改为暗色模式：
![方案调整](Snipaste_2025-09-20_22-52-19.png)
然后松开此处注释：
![页面设置](Snipaste_2025-09-20_22-48-54.png)
配置好后，重新打开本地网页：
``` bash
$ hexo clean && hexo g && hexo s
```
![主题配置](Snipaste_2025-09-20_22-53-49.png)
可以看到，主题已经更换为`next`的格式。关于主题的配置这里不作过多赘述，网络上关于`next`的主题配置美化教程有很多，可以自行尝试。
如果想写一篇新博客的话，首先最好将`_config.yml`中的`post_asset_folder`项改为`true`，并作如下修改：
![配置修改](Snipaste_2025-09-20_21-54-27.png)
这样我们在命令行创建新博客时会自动生成一个同名文件夹管理图片，命令行创建一篇新博客：
``` bash
$ hexo new "example"
```
然后在`source/_posts`目录下就会出现新创建的`markdown`文件和一个同名文件夹，只要将图片放在该文件夹中并以如下格式编写，就可以在博客中加入图片：
``` markdown
![图片](图片文件名)
```
![加入图片](Snipaste_2025-09-20_22-05-54.png)
如上图所示，成功加入图片并上传博客。

# 2.Vercel网站托管
首先在`GitHub`上创建一个仓库，我这里取名为`cyf-blog`，输入如下命令建立本地关联：
``` bash
$ git remote add origin git@github.com:magDice/cyf-blog.git
```
其中`magDice`替换为你的`GitHub`账户名，下一步把本地库的所有内容推送到远程库上
``` bash
$ git add .
$ git commit -m "first commit"
$ git branch -M main
$ git push -u origin main
```
成功之后，打开`Vercel`网页，选择导入我们`GitHub`的博客项目
![导入项目](Snipaste_2025-09-20_22-20-17.png)
![部署项目](sp20250920_135007_483.png)
`Framwork Preset`选择`Hexo`并部署，点击`Vercel`提供的域名即可访问我们的个人博客。
![直接访问](Snipaste_2025-09-20_22-45-18.png)
然而`Vercel`提供的域名需要科学上网才能访问，所以我们需要一个国内域名。随便购买一个国内域名，点击`Setting`，`Domains`，`Add Domain`。
![设置](Snipaste_2025-09-20_22-33-46.png)
这里输入购买的域名，然后点击`Save`。
![输入域名](Snipaste_2025-09-20_22-33-46.png)
进入域名控制台，我这里是腾讯云。选择域名点击解析，添加记录，如下图所示：
![配置1](Snipaste_2025-09-20_22-40-14.png)
然后再添加一条，如下所示：
![配置2](Snipaste_2025-09-20_22-41-44.png)
接下来稍等一会刷新页面，`Vercel`会自动检测，出现如下页面表示配置成功：
![成功](Snipaste_2025-09-20_22-43-19.png)
然后就可以通过国内域名直接访问了。
![国内域名访问](Snipaste_2025-09-20_22-46-12.png)