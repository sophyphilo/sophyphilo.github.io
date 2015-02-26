---
layout: post
title: "如何使用github和octopress搭建blog"
date: 2015-02-26 15:08:07 +0800
comments: true
categories: 
- 技术
- octopress
- github
---

  折腾了一些时间, 终于把blog在github上面搭建起来了, 非常感谢  
  <http://shengmingzhiqing.com/blog/octopress-tutorials-toc.html/> 这篇博文的作者.   
     
  `如何使用github和octopress搭建blog` 这个话题, 上面的博文已经讲得非常清晰了, 有兴趣的同学仔细研究那篇博文就可以, 我就不再废话了, 哈哈~~    
     
  下面主要说一下在搭建中遇到的问题以及那篇博文没有介绍的一些内容, 做个备忘:   

  <!--more-->

####1. 分类列表不支持中文
  按照 <http://shengmingzhiqing.com/blog/octopress-lean-modification-5.html/#section> 的方法制作分类目录的插件, 但是在 `rake generate` 后, 出现如下错误:   

  {% codeblock %}
  Liquid error: incompatible encoding regexp match (ASCII-8BIT regexp with UTF-8 string)
  {% endcodeblock %}

  最终在这里 <http://pfmiles.github.io/blog/liquid-error-about-regexp-match-when-using-octopress-tagcloud/> 找到了答案, 我采用了第二种方法, 在正则式后加上u选项, 将

  {% codeblock %}
  category_url = File.join(category_dir, category.gsub(/_|\P{Word}/, '-').gsub(/-{2,}/, '-').downcase)
  {% endcodeblock %}

  改为

  {% codeblock %}
  category_url = File.join(category_dir, category.gsub(/_|\P{Word}/u, '-').gsub(/-{2,}/u, '-').downcase)
  {% endcodeblock %}

####2. 如何加快blog的访问速度
  历经千辛万苦搭建完blog, 很兴奋的用markdown写篇测试博文, `rake deploy`, 在chrome中浏览却发现加载页面的速度慢如蜗牛......, 看了看_config.yml, 瞥见了google plus, twitter, 万恶的GFW......   
  看[这里][], 经过一番清理, 提速不少~~

[这里]:http://droidyue.com/blog/2014/06/22/fix-octopress-slow-loading-speed-issue-in-china-mainland/


####3. 在侧边栏添加访客地图

  使用第三方提供的服务, 从[这里][earth]获取js代码.  

#####3.1 在 source/_includes/custom/asides/ 路径下添加visitor.html
  {% codeblock source/_includes/custom/asides/visitor.html %}
  <section>
      <h1>访客地图</h1>
          <script type="text/javascript" src="//rj.revolvermaps.com/0/0/1.js?i=9ojojv7pf1u&amp;s=220&amp;m=0&amp;v=true&amp;r=false&amp;b=000000&amp;n=false&amp;c=ff0000" async="async"></script>
  </section>
  {% endcodeblock %}

#####3.2 将visitor.html加入主页面
  修改_config.yml, 将visitor.html 加入 `default_asides`.

  {% codeblock _config.yml中的default_asides %}
  default_asides: [custom/asides/category_list.html, asides/recent_posts.html, custom/asides/visitor.html]
  {% endcodeblock %}

[earth]:http://www.revolvermaps.com/?target=setup

####4. 添加评论系统
   我没有使用Octopress默认的Disqus, 国内比较常用的有 `多说` 和 `友言`, 我采用了 `友言` .
   具体配置详情见[这里][comment].

[comment]:http://pangyi.github.io/blog/20150125/shi-yong-you-yan-zuo-octopressde-ping-lun-xi-tong-,shi-yong-jia-wang-zuo-fen-xiang/





