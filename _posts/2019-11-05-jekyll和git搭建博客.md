---
layout: post
title: 'jekyll 和git 搭建博客(极其简单的方法,套模板)'
date: 2019-11-05
categories: test
tags: jekyll
---

- (前提需要下载安装好git和jekyll)

- 1.创建githup 账号,并新建仓库![](/images/搭建博客/sendpix0.jpg)

  

- 2.在Linux终端里写入clone命令 git clone https://github.com/sum-del/sum-del.github.io(这是我本人的库名)或者通过gitup库里下载,自己的库![](/images/搭建博客/搭建博客2.jpg)

- \3. 下载模板[http://jekyllthemes.org/],更改配置文件_config.yml,这里面更改url地址为http://+你的库名,_posts 这里存放要发表的文章，也就是需要被转换成.html的.md文件

- 4.我比较懒,就把修改后的文件复制到自己仓库的文件中,

- 5.终端cd 进入这个克隆的文件当中,打开jekyll server ,在本地浏览器输入http://localhost:4000：可以预览效果

- 6.效果满意进入终端上传文件

- 7.4步上传

  - \1. git add .
  - \2. git commit
  - 3.git pull
  - 4.git push

- 完成博客,点击网站查看即可