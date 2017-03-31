---
layout: post
title: "Jekyll实践: Github Pages"
categories: jekyll
---
# {{ page.title }}
---
>**简介**: 最近了解了一个名为 `liquid` 的模板引擎，
发现 [**jekyll**](https://jekyllrb.com/) 使用的就是这个模板引擎，
而 github pages 就是用 jekyll 来建立的。
所以就来试着搞个 github pages 吧！
的本篇并不拘泥于详尽的搭建教程，
不过是记录了一下作者在搭建的过程中的一些信息,
具体的步骤参见官方文档就好了。

## **---1---  github.io --> jekyll**

#### 如果只是想搭建一个最简单的 github.io 页面，只要：
  - 根据官方文档的步骤创建一个 repo
  - 设定一个主题风格
  - 在 README.md 编辑 markdown 格式的内容

#### 如果要做复杂一点的界面，并且做一些定制，那么就要：
 - 搭建 jekyll 的基础环境(这步对于 Ruby 开发者是很轻松的)
   - `ruby`
   - `bundler`
   - `git clone git@your_github_io_repo.git` 
   - 添加 `Gemfile` [(e.g.)](https://github.com/mccg/mccg.github.io/blob/master/Gemfile)
   - `bundle install`
 - 阅读 [jekyll 的文档](https://jekyllrb.com/docs/home/)
 - 完成开发环境代码
 - `git push origin master`

>##### 关于 `markdown`:
 - :clipboard: [markdown-cheetsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
 - :pencil: [markdown-online-editor](https://jbt.github.io/markdown-editor/)
 - :smiling_imp: [emoji-cheet-sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet/)

---
## **---2---  完成 jekyll 开发环境的代码**

### 开启站点服务：`bundle exec jekyll serve` 
 - 本地服务成功启动后，默认访问的地址是 `http://localhost:4000/`，
如果需要从其他地址来访问站点，
可以在 `_config.yml` 文件中设置 `host: 0.0.0.0`，
然后访问 `http://xxx.xxx.xxx.xxx:4000/` 即可。

### CSS 样式
 - Blog 的主题样式既可以通过设置 `_config.yml` 中的 `theme` 选项配置现有支持的主题，
也可以自己编写并添加在相应的位置上。

>#### Q: 如何覆盖原来的主题中的样式？
A: 请参见[此链接](http://stackoverflow.com/questions/41254582/overriding-css-on-github-pages-using-slate-theme)，
但是请注意**好像**只有这一种方法能奏效，我本想替换为格式更优美一点的 `Sass`, 然而并没有成功:broken_heart:……

>### 未完待续...


