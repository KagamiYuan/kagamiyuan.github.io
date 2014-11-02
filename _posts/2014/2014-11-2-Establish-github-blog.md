---
layout: post
title: 代码初学者建立github博客
categories:
- github
tags:
- github
- jekyll
---


#背景
上大学的时候写博客用的微软的Windows live space记录生活，关闭后微软安排搬到了wordpress.com， 同时在bloodspot上开个了博客放自己在译言和豆瓣的公开文章。毕业回国后两个博客网站都被墙了，从此断了写博客的念头。

现在在coursera上断断续续学了一年的R([Data science specilization @ JHU](https://www.coursera.org/specialization/jhudatascience/1?utm_medium=listingPage))，觉得很有趣味，同时学会了用github，就计划在github上开个技术博客，记录敲代码的学习经历和做专利的生活。

后天(2014.11.3)就要开始去金杜律师事务所进行专利代理实习生的工作了，希望能顺利度过4个月并留用。

#过程
##概要
我没有学过ruby，没有学过自己架博客，wordpress下载了也不会用，github到现在都只会用客户端而不会用命令，没有学过jekyll，html只是前几天在w3school上粗略过了一遍，只能以小白的理解方法描述github博客搭建过程。

github博客简单讲就是在github（一个类似百度云的网站，可以存放一些文件）上建立一个固定命名格式的文件夹，在其中上传一些固定要求的各种格式的文本文件，github就会自动提供一个公共链接，访问这个公共链接就可以打开博客。

所以问题就简化成：向github上传一些文本文件，根据这些文件，github自动生成了博客。

这些文件又可以分成两类：

* 一类是用来描述博客外观的文件（包含博客的格式、字体、颜色、组成部分等）；
* 另一类就是博客文章。

在[jekyllthemes](http://jekyllthemes.org)网站上，可以看到若干种博客主题，下载下来后会发现都是一些文件，把这些文件上传到自己的github上，就可以建立相同的博客了。之后，再根据自己的需要，对博客外观进行调整，并发表自己的博客文章了。

##环境和工具
* Macbook Air 13 inch 128GB，1.3G Core i5, 4G 1600MHz DDR3
* OS X 10.9.5   
* 通过邮箱验证的github帐号，及github客户端，学习github基础知识
* OS X自带的ruby环境（自带的，不用安装）
* jekyll (ruby package，需自行安装)   
* 网上的jekyll theme博客主题模板（问google和百度）
* sublime text2（mac下的文本编辑器，在这里用于编辑html和yml文件）
* mou（mac下的markdown编辑器，在这里用于编辑md文件），学习markdown基础知识
* [w3school](http://w3school.com.cn)学习html的基础知识


##安装jekyll
jekyll是一个ruby（一种编程语言）的程序。mac一般已经自带ruby环境，可以进入terminal程序，输入

```
$ ruby --version
```
检查自带的ruby版本

```
ruby 2.0.0p481 (2014-05-08 revision 45883) [universal.x86_64-darwin13]
```

随后，安装ruby环境下的bundler程序，输入

```
$ gem install bundler
```

由于网络问题，可能会显示无法访问[ruby](https://rubygems.org)网站下载程序。可以输入

```
$ gem sources -a http://ruby.taobao.org/
```
增加下载ruby程序的源，并使用`gem sources -l`查看。

如果还是下载失败，可以直接访问[ruby](https://rubygems.org)，搜索bundler，下载到本地进行安装。

```
$ cd bundler程序所在的文件夹
$ gem install 下载得到的bundler文件名 --l
```

安装时可能会出现“你没有权限修改ruby文件夹”的警告，可以输入

```
$ sudo chmod 777 /Library/Ruby/Gems/2.0.0
```
来获得ruby文件夹的root权限。如果输入命令后反应很慢，可以用笨办法开启root帐号并登录，进行本地安装。具体可以参见[apple官方指导开启root账户](http://support.apple.com/kb/HT1528?viewlocale=zh_CN&locale=zh_CN)。并顺便在root账户下安装jekyll

```
$ gem install jekyll
```

到此，jekyll程序就安装完成了。

##选择一个jekyll博客主题并安装
网上有很多jekyll博客主题，以我所用的[Jim的模板](https://github.com/dashjim)为例，访问他的github账户，jekyll博客主题对应的repository的固定格式文件夹名称为`USERNAME.github.com`或`USERNAME.github.io`，我观察了下现在似乎都统一成io后缀了。

点右上角Fork，将他的文件夹搬运到自己的github下后，点右侧的Setting，修改Repository name为自己的`USERNAME.github.io`，同时应该已经可以看到页面下面有一条信息

```
 Your site is published at http://USERNAME.github.io.
 ```
访问该链接，即可访问你的博客了。不过在第一次建立博客时，github需要10min左右的缓冲时间来建立。

返回到前一页面，点右侧的Clone in Desktop，将这个文件夹连同里面的所有文件下载到本地硬盘，以方便编辑。

在拥有了自己的博客文件夹`USERNAME.github.io`后，通过在terminal中输入`jekyll serve`命令来在本地预览自己的博客。

```
$ cd USERNAME.github.io所在路径
$ jekyll serve
```

程序会自动在[http://0.0.0.0:4000/](http://0.0.0.0:4000/)建立本地的博客预览，访问该链接即可预览博客，按`ctrl-c`来结束博客预览。

在修改了文件夹内容后，先结束博客预览，再通过`jekyll serve`命令来重新建立新的博客预览。没有问题了，再上传到github网站上。

##jekyll博客文件夹中的各文件用途
USERNAME.github.io文件夹中的一个文件`_config.yml`和两个文件夹`_layouts`，`_posts`是重要的。

###_config.yml文件
`_config.yml`可以用sublime text2程序来打开并编辑，其中的内容可能会被其他页面所引用。

```
#所使用的markdown解析器
markdown: redcarpet
#大概是指文章链接格式为年-月-标题
permalink: /:year/:month/:title/
#描述作者，会在其他页面中引用到
author: Yuan Yuan
#代码高亮
highlighter: pygments
#paginate指定一页有几篇文章
paginate: 24
```


###_layouts文件夹
`_layouts`文件夹中，包含各网页的模板，例如本文所述模板中包含`default.html`，`page.html`，`post.html`三个文件。`default.html`为最基本的默认模板，`page.html`和`post.html`均在自己文件的开端通过

```
---
layout: default
---
```
来引用default模板。

以`page.html`为例，在显示除博客文章以外的页面时载入：

```
---
<--!使用default模板-->
layout: default
---

<--!本页面自带的内容为content-->
<section class="post">
{{ content }}
</section>

<--!如果本页面带有评论功能，那么同时载入comments.md-->
{% if page.comments %}
{% include comments.md %}
{% endif %}
```

以`post.html`为例，在显示博客文章时载入：

```
---
<--!使用default模板-->
layout: default
---

<--!本页面自带的内容为content，在页面上表现为博客文章-->
<section class="post">
{{ content }}
</section>
< hr /><--!水平分割线，为了在markdown下正常显示该代码，在h前加了一个空格-->

<--!博客文章下面的内容，在页面上表现为作者author，许可license，分类categories，标签tags和时间time-->
<section class="meta">

<--!作者信息-->
<span class="author">
  <a href="http://kagamiyuan.github.com">{{ site.author }}</a> - 专利律师实习生，北京金杜律师事务所。
</span>
<br />

<--!文章发布许可-->
<span class="license">
  Published under <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">(CC) BY-NC-SA</a>
</span>

<--!如果该文章有分类-->
{% if page.categories %}
<span class="categories">
  in categories
  {% for cat in page.categories %}
  <a href="/categories/#{{ cat }}" title="{{ cat }}">{{ cat }}</a>&nbsp;
  {% endfor %}
</span>
{% endif %}

<--!如果该文章有标签-->
{% if page.tags %}
<span class="tags">
  tagged with 
  {% for tag in page.tags %}
  <a href="/tags/#{{ tag }}" title="{{ tag }}">{{ tag }}</a>&nbsp;
  {% endfor %}
</span>
{% endif %}

<--!发表时间-->
<span class="time">
  <br/>
  <time datetime="{{ page.date | date:"%Y-%m-%d" }}">{{ page.date | date:"%Y-%m-%d" }}</time>
</span>
</section>

<--!其他略-->
```
###_post文件夹
`_post`文件夹中存放着markdown格式的博客文章，文件名按照固定格式为

```
2014-11-2-Establish-github-blog.md
```
文章开头通过

```
---
layout: post
title: 代码初学者建立github博客
categories:
- github
tags:
- github
- jekyll
---
```
表明该文章应采用`post.html`模板，并描述了文章标题、分类和标签。

之后按照正常markdown语法撰写正文即可，文章标题就不用在正文部分再写一遍了。

#结论
这个博客的结构构成为：

1. 主页Index
2. 文章分类 Categories
3. 文章标签 Tags
4. 留言 Comments
5. 关于我 About me
6. 订阅RSS

其中1~5均引用的`page.html`模板，即`default.html`模板+页面内容content+可能的comment。

博客文章引用的`post.html`模板，即`default.html`模板+页面内容content+作者+许可+分类+标签+时间+评论+分享+跳转。

具体`default.html`中如何设置页面格式，还有待进一步研究。