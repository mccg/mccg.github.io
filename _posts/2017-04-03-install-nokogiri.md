---
layout: post
title: "安装 Nokogiri"
category: Dev
tags: ["ruby"]
date: 2017-04-03

---

>**引言**: 
截止到目前为止，
基本上每次搭建或部署与 nokogiri 这个 gem 有关的项目的环境的过程中，
都会遇到 nokogiri 编译失败的问题。

因为 nokogiri 的编译要依赖 libxml2 和 libxslt 这两个项目，
所以，如果这两个项目的路径没有配置”正确”， 
就会发生 nokogiri 的编译失败。

所以如果遇到了编译问题，很有必要看一下 nokogiri 的官方网站给出的[安装指南](http://www.nokogiri.org/tutorials/installing_nokogiri.html)。

