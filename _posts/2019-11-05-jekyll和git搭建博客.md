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

- \3. [下载模板](http://jekyllthemes.org/),更改配置文件_config.yml,这里面更改url地址为http://+你的库名,_posts 这里存放要发表的文章，也就是需要被转换成.html的.md文件

- 4.我比较懒,就把修改后的文件复制到自己仓库的文件中,

- 5.终端cd 进入这个克隆的文件当中,打开jekyll server ,在本地浏览器输入http://localhost:4000：可以预览效果

- 6.效果满意进入终端上传文件

- 7.4步上传

  - \1. git add .
  - \2. git commit
  - 3.git pull
  - 4.git push

- 完成博客,点击网站查看即可

## 下面是经常遇到的一些问题

### 1. 本地不能访问

### 问题描述：

在浏览器中不能查看本地效果

```cpp
http://localhost:4000
```

### 解决方法：

检查_config.yml配置文件是否需要修改

### 2. Jekyll3.0不能编译

### 问题描述：

```csharp
Deprecation: You appear to have pagination turned on, but you haven’t included the jekyll-paginate gem. Ensure you have gems: [jekyll-paginate] in your configuration file.
```

### 故障原因：

jekyll自3.0版本以后不再支持相对路径，统一用绝对路径。

### 解决方法：

（1）打开_config.yml文件，将relative_permailinks:true注释掉;

在结尾添加

```css
gems: [jekyll-paginate]
```

保存；

（2）接下来安装缺失的插件：

```css
gem install pygments.rb

gem install redcarpet
```

现在编译Jekyll build

### 3. 下载认证文件

```python
curl http://curl.haxx.se/ca/cacert.pem -o cacert.pem
```

设置环境变量，重新安装

## 常见报错 ：

### 错误提示1.

```python
  Dependency Error: Yikes! It looks like you don't have bundler or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- bundler' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
jekyll 3.5.0 | Error:  bundler
```

安装bundler

```python
gem install bundler
```

###  错误提示2.

```python
 Could not find gem 'minima (~> 2.0) x64-mingw32' in any of the gem sources listed in your Gemfile. (Bundler::GemNotFound)
```

安装Ruby环境

```python
 gem install minima
```

#### 错误提示3:

```python
   Deprecation: The 'gems' configuration option has been renamed to 'plugins'. Please update your config file accordingly.
```

配置文件_config.yml中，使用了 plugins 的配置项，应该是用plugins替换掉gems,也有可能gems 和plugins 同时存在了

### 错误提示4.

```python
   Configuration file: /_config.yml
            Source: .
       Destination: ./_site
      Generating...
                    done.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for '.'
Configuration file: /_config.yml
jekyll 2.4.0 | Error:  Permission denied - bind(2) for 127.0.0.1:4000
```

使用 netstat 命令查看各种端口的被进程的占用情况，通过

```python
tasklist /svc /FI "PID eq 11476"
```

查看具体哪一个进程占用，也可借助于第三方工具完成。

