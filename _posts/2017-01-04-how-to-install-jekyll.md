---
layout: post
title: "Jekyll搭建博客"
description: "使用Jekyll搭建自己的博客站点."
tags: [jekyll]
---

**Jekyll**是一个简单的免费的Blog生成工具，类似WordPress。但是和WordPress又有很大的不同，原因是jekyll只是一个生成静态网页的工具，不需要数据库支持。但是可以配合第三方服务,例如Disqus。最关键的是jekyll可以免费部署在Github上，而且可以绑定自己的域名。

安装 Jekyll 相当简单，开始前你需要确保系统里已经有如下配置。

- **Ruby**
- **RubyGems**
- **Linux, Unix, or Mac OS X**

-------------------

* TOC
{:toc}

## 安装Ruby

> Ruby 是一种面向对象、命令式、函数式、动态的通用编程语言。在20世纪90年代中期由日本人松本行弘（Matz）设计并开发。遵守BSD许可证和Ruby License。它的灵感与特性来自于Perl、Smalltalk、Eiffel、Ada以及Lisp语言。    —— [维基百科](https://zh.wikipedia.org/wiki/Ruby)

### 源码安装Ruby
```powershell
$ wget http://cache.ruby-lang.org/pub/ruby/ruby-2.3.3.tar.gz
$ tar zxvf ruby-2.3.3.tar.gz
$ cd ruby-2.3.3
$ ./configure --prefix=/usr/local/ruby --with-opessl-dir=/root/soft/openssl-1.0.0l
$ make && make install
$ echo "export PATH=/usr/local/ruby/bin:$PATH >> ~/.bash_profile"
$ source ~/.bash_profile
$ ruby --version
```
### 安装gem并更新gem源
```powershell
$ wget https://rubygems.org/rubygems/rubygems-2.6.8.tgz
$ tar zxvf rubygems-2.6.8.tgz
$ cd rubygems-2.6.8
$ ruby setup.rb
$ gem --version
```
### 更换gem源为RubyChina

RubyGems 一直以来在国内都非常难访问到，在本地你或许可以翻墙，当你要发布上线的时候，你就很难搞了 [Ruby China](http://ruby-china.org/) 社区提供了一个完整的 [RubyGems](https://gems.ruby-china.org/) 镜像，这个镜像基于国内 CDN + 国外服务器的方式，能确保几乎无延迟的同步。

```powershell
# 更新RubyGems版本，官方建议 2.6.x ，如果是参照上一步安装的gem源，可以跳过此步
$ gem update --system # 这里请翻墙一下
$ gem -v

# 开始更换gem源
$ gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
$ gem sources -l # 确保只有 gems.ruby-china.org
```
> **提示：**如果遇到 SSL 证书问题且无法解决，请直接用 http://gems.ruby-china.org 避免 SSL 的问题。

## 安装Bundle 
```powershell
$ gem install bundler
# 更改Bundle源
$ bundle config mirror.https://rubygems.org https://gems.ruby-china.org
# 或者直接更换项目中Gemfile文件的source
$ vim Gemfile
# 更换 source为 https://gems.ruby-china.org
```
## 安装Jekyll
```powershell
$ gem install jekyll
$ jekyll new  my-awesome-site
$ cd  my-awesome-site
$ jekyll serve # 启动完毕后浏览器访问http://127.0.0.1:4000
# jekyll serve 增加 --detach 参数后，会脱离终端在后台运行。
```
>**提示**如果想关闭服务器，可以使用`kill -9 PID`命令，如果找不到PID，可以使用`ps aux | grep jekyll`命令查看。