---
layout: post
title: "gitk的命令行替代工具"
date: 2015-02-26 20:05:35 +0800
comments: true
categories: 
- git
---

  `gitk` 是一个非常好用的帮助理清 `git` 分支间关系和 查看仓库历史的图形化工具.     
  但是如果没有GUI支持的时候 (比如git仓库在远程主机上 而且本机没有 `X11` 支持), 此时该如何查看仓库历史才能达到 `gitk` 的效果呢?   

  <!--more-->

  `git log --graph` 加上几个选项可以达到 `gitk` 类似的效果:

	git log --graph --abbrev-commit --pretty=oneline --decorate

  `--abbrev-commit` : 显示缩略的提交ID    
  `--pretty=oneline` : 一行显示一个提交   
  `--decorate` : 显示出提交对应的ref名称    

------------------------
  
**gitk 运行结果截图:**    
  <img src="/images/blog_images/gitk-image.png" width="550" height="650"> 

**git log运行结果截图:**  
  <img src="/images/blog_images/git-log-image.png" width="550" height="650"> 

