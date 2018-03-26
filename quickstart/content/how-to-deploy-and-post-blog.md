---
title: "如何部署并添加文章"
date: "2015-08-24"
description: "如何使用 hugo 添加新的文章"
categories: 
    - "hugo"
---
部署
====

我们采用的blog部署步骤:

首先你安装一下[hugo](http://gohugo.io/tutorials/github-pages-blog/),安装非常简单，例如，如果你是window的用户，只要下载对应版本的 exe文件，然后将这个文件路径加入到你的环境变量`path`中，然后再cmd窗口，敲打hugo，试试有没有反应。如果一切顺利，我们就可以继续下面的步骤了，所有的步骤在上面给的链接里面都有，我只是加了我在部署的时候，补充了一些说明:

1. 建立一个github 名为 `youproject-hogo`，用于存储hogo内容，包括部署文件，模板主题；


+ 建立一个github 名为`username.github.io'必须是和你的github用户名一样的库，用于发布通过hogo生成的静态网页，这个可以为空;

+ `git clone <<your-project>-hugo-url> && cd <your-project>-hugo`在本地克隆项目，并进入项目目录;

+ 在`youproject-hogo`目录中，建立初始的目录结构,类似于[`hogo_gh_blog`](https://github.com/spencerlyon2/hugo_gh_blog)建议拷贝这个目录结构，不要public目录，然后修改一下`config.yaml`文件(在文件末尾添加`canonifyurls: true`)和`deploy.sh`文件，这个后面会讲到;


+添加新博文，想想本地运行效果的,可运行`hugo server --watch -t <yourtheme>`没有theme话，默认为空，这个时候，就可以看在post下的md文件修改之后，生成的index.html的样子，会自动在public下生成，当你修改满意之后，浏览器访问http://127.0.0.1:1313/，就可以访问自己的网站。选择`ctrl+c`退出watch模式。这个时候删除public文件夹，rm -rf public这个很重要，如果不删除，将导致下一步命令不成功;


+ 运行`git submodule add git@github.com:<username>/<username>.github.io.git public`这句话的意思是将当前目录下建一个public的文件夹，然后添加到`<username>.github.io.git`中，这样的效果就是，public下的文件提交，可以直接提交到`<username>.github.io.git`,这样我们就可以完成在`youproject-hogo`项目中生成public，然后将public下的文件发布到`<username>.github.io.git`;


+ 最后我们修改下这个`deploy.sh`文件，运行bash deploy.
<pre>```
	#!/bin/bash
	echo -e "\033[0;32mDeploying updates to Github...\033[0m"
	#Build the project.
	hugo
	cd public
	#Add changes to git.
	git add -A
	#Commit changes.
		msg="rebuilding site `date`"
	if [ $# -eq 1 ]
  		then msg="$1"
	fi
	git commit -m "$msg"
	#Push source and build repos.
	git push origin master
	cd ..
```
</pre>


允许之后，public下的东西就提交到了`<username>.github.io.git`.

别忘了，之后也提交一下hugo的项目

如何添加新博文
============

部署完之后，每次添加新博文只要在post下面编写md文件，hugo编译之后，运行如下命令，完成复制并提交到`<username>.github.io.git`。

	bash deploy.sh "message"

如果不小心删除了public文件夹下的 git 目录，可以先删除整个`public`目录，然后使用
<pre>
```git rm -rf --cached public
```
</pre>
先将public从cached中删除,然后运行
<pre>
```git submodule --force add git@github.com:lynn8570/lynn8570.github.io.git public
```
</pre>
这样在编译hugo之后，提交public的文件又可以重新提交到github.io上了




