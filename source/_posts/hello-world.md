---
title: Hello World
tags: 博客
categories: 博客
---
这是我博客的第一篇文章，记录搭建博客的过程。。。

[Hexo](https://hexo.io/zh-cn/) 是高效的静态站点生成框架，她基于 [Node.js](https://nodejs.org/)。 通过 Hexo 你可以轻松地使用 Markdown 编写文章，除了 Markdown 本身的语法之外，还可以使用 Hexo 提供的 [标签插件](https://hexo.io/zh-cn/docs/tag-plugins.html) 来快速的插入特定形式的内容。在这篇文章中，假定你已经成功安装了 Hexo，并使用 Hexo 提供的命令创建了一个站点。

<!--more-->

# 准备工作

- GitHub账号
- 安装node.js、npm
- 安装git for windows

# 使用Hexo写博客

## Hexo简介

Hexo是一个简单、快速、强大的基于 Github Pages 的博客发布工具，支持Markdown格式，有众多优秀插件和主题。

官网： [http://hexo.io](http://hexo.io/) github: https://github.com/hexojs/hexo

## 原理

由于github pages存放的都是静态文件，博客存放的不只是文章内容，还有文章列表、分类、标签、翻页等动态内容，假如每次写完一篇文章都要手动更新博文目录和相关链接信息，相信谁都会疯掉，所以hexo所做的就是将这些md文件都放在本地，每次写完文章后调用写好的命令来批量完成相关页面的生成，然后再将有改动的页面提交到github。

## 注意事项

- 很多命令既可以用Windows的cmd来完成，也可以使用git bash来完成，但是部分命令会有一些问题，为避免不必要的问题，建议全部使用git bash来执行；
- hexo不同版本差别比较大，网上很多文章的配置信息都是基于2.x的，所以注意不要被误导；
- hexo有2种_config.yml文件，一个是根目录下的全局的_config.yml，一个是各个theme下的；

## 安装

在你电脑桌面右键鼠标，选择Git Bash Here

```
$ npm install -g hexo
```

## 初始化

在电脑的某个地方新建一个名为hexo的文件夹（名字可以随便取），比如我的是F:\Workspaces\hexo，由于这个文件夹将来就作为你存放代码的地方，所以最好不要随便放。

```
$ cd /f/Workspaces/hexo/
$ hexo init
```

hexo会自动下载一些文件到这个目录，包括node_modules，目录结构如下图：

{% asset_img 1.png This is an example image %}

```
$ hexo g # 生成
$ hexo s # 启动服务
```

执行以上命令之后，hexo就会在public文件夹生成相关html文件，这些文件将来都是要提交到github去的：

{% asset_img 2.png This is an example image %}

`hexo s`是开启本地预览服务，打开浏览器访问 http://localhost:4000 即可看到内容，很多人会碰到浏览器一直在转圈但是就是加载不出来的问题，一般情况下是因为端口占用的缘故，因为4000这个端口太常见了，解决端口冲突问题请参考这篇文章：http://blog.liuxianan.com/windows-port-bind.html

## 修改主题

既然默认主题很丑，那我们别的不做，首先来替换一个好看点的主题。这是 [官方主题](https://hexo.io/themes/)。

个人比较喜欢的2个主题：[hexo-theme-jekyll](https://github.com/pinggod/hexo-theme-jekyll) 和 [hexo-theme-yilia](https://github.com/litten/hexo-theme-yilia)。

首先下载这个主题：

```
$ cd /f/Workspaces/hexo/
$ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
```

下载后的主题都在Themes文件夹里

修改_config.yml中的theme: landscape改为theme: yilia，然后重新执行hexo g来重新生成。

如果出现一些莫名其妙的问题，可以先执行hexo clean来清理一下public的内容，然后再来重新生成和发布。

## 上传之前

在上传代码到github之前，一定要记得先把你以前所有代码下载下来（虽然github有版本管理，但备份一下总是好的），因为从hexo提交代码时会把你以前的所有代码都删掉。

## 上传到github

如果你一切都配置好了，发布上传很容易，一句hexo d就搞定，当然关键还是你要把所有东西配置好。

首先，ssh key肯定要配置好。

其次，配置_config.yml中有关deploy的部分：

正确写法：

```
deploy:
  type: git
  repository: git@github.com:liuxianan/liuxianan.github.io.git
  branch: master
```

如果报错：

```
Deployer not found: github 或者 Deployer not found: git
```

需要安装插件：

```
npm install hexo-deployer-git --save
```

## 常用的Hexo命令

```
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #部署到GitHub
hexo help  # 查看帮助
hexo version  #查看Hexo的版本
```

缩写：

```
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
```

组合命令：

```
hexo s -g #生成并本地预览
hexo d -g #生成并上传
```

## 写博客

定位到我们的hexo根目录，执行命令：

```
hexo new 'my-first-blog'
```

hexo会帮我们在_posts下生成相关md文件：

完整格式如下：

```
---
title: postName #文章页面上的显示名称，一般是中文
date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: 默认分类 #分类
tags: [tag1,tag2,tag3] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: 附加一段文章摘要，字数最好在140字以内，会出现在meta的description里面
---
```

## 图片问题

首先我们需要安装一个图片路径转换的插件，这个插件名字是**hexo-asset-image**

```
npm install https://github.com/CodeFalling/hexo-asset-image --save
```

但是这个插件的内容需要修改【不然可能会出Bug】

打开/node_modules/hexo-asset-image/index.js，将内容更换为下面的代码：

```js
'use strict';
var cheerio = require('cheerio');

// http://stackoverflow.com/questions/14480345/how-to-get-the-nth-occurrence-in-a-string
function getPosition(str, m, i) {
  return str.split(m, i).join(m).length;
}

var version = String(hexo.version).split('.');
hexo.extend.filter.register('after_post_render', function(data){
  var config = hexo.config;
  if(config.post_asset_folder){
    	var link = data.permalink;
	if(version.length > 0 && Number(version[0]) == 3)
	   var beginPos = getPosition(link, '/', 1) + 1;
	else
	   var beginPos = getPosition(link, '/', 3) + 1;
	// In hexo 3.1.1, the permalink of "about" page is like ".../about/index.html".
	var endPos = link.lastIndexOf('/') + 1;
    link = link.substring(beginPos, endPos);

    var toprocess = ['excerpt', 'more', 'content'];
    for(var i = 0; i < toprocess.length; i++){
      var key = toprocess[i];
 
      var $ = cheerio.load(data[key], {
        ignoreWhitespace: false,
        xmlMode: false,
        lowerCaseTags: false,
        decodeEntities: false
      });

      $('img').each(function(){
		if ($(this).attr('src')){
			// For windows style path, we replace '\' to '/'.
			var src = $(this).attr('src').replace('\\', '/');
			if(!/http[s]*.*|\/\/.*/.test(src) &&
			   !/^\s*\//.test(src)) {
			  // For "about" page, the first part of "src" can't be removed.
			  // In addition, to support multi-level local directory.
			  var linkArray = link.split('/').filter(function(elem){
				return elem != '';
			  });
			  var srcArray = src.split('/').filter(function(elem){
				return elem != '' && elem != '.';
			  });
			  if(srcArray.length > 1)
				srcArray.shift();
			  src = srcArray.join('/');
			  $(this).attr('src', config.root + link + src);
			  console.info&&console.info("update link as:-->"+config.root + link + src);
			}
		}else{
			console.info&&console.info("no src attr, skipped...");
			console.info&&console.info($(this));
		}
      });
      data[key] = $.html();
    }
  }
});
```

打开_config.yml文件，修改下述内容

```
post_asset_folder: true
```

Hexo 提供了一种更方便管理 Asset 的设定：post_asset_folder当您设置post_asset_folder为true参数后，在建立文件时，Hexo会自动建立一个与文章同名的文件夹，您可以把与该文章相关的所有资源都放到那个文件夹。

在需要图片的地方插入代码：example.jpg为图片名称

```
{% asset_img example.jpg This is an example image %}
```

