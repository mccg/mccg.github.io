---
layout: post
title: "jekyll 实践: Github Pages"
category: Dev
tags: ["jekyll", "web"]
date: 2017-03-30
comments: true

---

>**引言**:
最近了解了一个名为 `liquid` 的模板引擎，
发现 [**jekyll**](https://jekyllrb.com/) 使用的就是这个模板引擎引言而 github pages 就是用 jekyll 来驱动的。
所以就使用 jekyll 来试着搞个 github pages 吧！
的本篇并不拘泥于详尽的搭建教程，
不过是记录了一下作者在搭建的过程中的一些信息,
具体的步骤参见官方文档就好了。


## **1  github.io ( 使用 jekyll )**

- #### 如果只是想搭建一个最简单的 github.io 页面，只要：
    - 根据官方文档的步骤创建一个 repo
    - 设定一个主题风格
    - 在 README.md 编辑 markdown 格式的内容

- #### 如果要做复杂一点的界面，并且使用 jekyll 做一些定制，那么就要进行如下步骤：
    - ``1.`` 搭建 jekyll 的基础环境(这步对于 Ruby 开发者是很轻松的)
      - 安装 Ruby
      - 安装 gem 和 bundler
      - `git clone git@your_github_io_repo.git`
      - 添加 `Gemfile` [(e.g.)](https://github.com/mccg/mccg.github.io/blob/master/Gemfile)
      - `bundle install`
    - ``2.`` 阅读 [jekyll 的文档](https://jekyllrb.com/docs/home/)
    - ``3.`` 完成开发环境代码
    - ``4.`` `git push origin master`

- >##### 关于 `markdown`:
  >- :clipboard: [markdown-cheetsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
  >- :pencil: [markdown-online-editor](https://jbt.github.io/markdown-editor/)
  >- :smiling_imp:  [emoji-cheetsheet](https://www.webpagefx.com/tools/emoji-cheat-sheet/)

- >##### 关于 `Hexo`:
  github pages 同样可以使用 `Hexo` 来搭建，
  主要步骤就是按 `Hexo` 的规则编辑完模板后，
  使用模板引擎先导出为 .html 文件，
  (在 `jekyll` 中，默认的导出文件夹是 `_site`)
  然后将这些文件 push 到 github repository 上。

## **2 完成 jekyll 开发环境的代码**

- ### 启动站点服务：`bundle exec jekyll serve`
  - 本地服务成功启动后，默认访问的地址是 `http://localhost:4000/`，
  - 在自己的浏览器中就可以访问，
    如果你的开发环境需要从其他地址来访问站点，
    可以在 `_config.yml` 文件中设置 `host: 0.0.0.0`，
    然后访问 `http://xxx.xxx.xxx.xxx:4000/` 即可,
    当然这里的 `4000` 的端口号也是可以通过配置修改的。

- ### CSS 样式
  - Blog 的主题样式既可以通过设置 `_config.yml` 中的 `theme` 选项配置现有支持的主题，
    也可以自己编写并添加在相应的位置上。

  - >#### Q: 如何覆盖原来的主题中的样式？
    A: 请参见[此链接](http://stackoverflow.com/questions/41254582/overriding-css-on-github-pages-using-slate-theme)，
    但是请注意**好像**只有这一种方法能奏效，我本想替换为格式更优美一点的 `Sass`, 然而并没有成功:broken_heart:……

- ### 模板中的 `Front Matter` 标记
  - 两个三横线是模板文件前置的标记，
    其实 `---`也是 `YAML` 文件的默认的起始符号，
    你可以在**任何**模板文件中使用 `Front Matter` 格式。比如：
    ```
    ---
    【此部分为 YAML 格式的数据】
    ---
    【此部分为模板的内容。】
    【具体按照的何种格式读取解析，】
    【是要根据当前模板文件的后缀名来决定。】
    ```

## **3 jekyll plugins**

- jekyll 支持在 `_config.yml` 文件中通过配置 `plugins` 来配置插件。
  也可以将 `*.rb` 插件写在 `_plugins` 文件夹下，或者通过安装 Gem 来引用 ruby 代码，
  jekyll 启动的时候会先加载 `_plugins` 中的代码。
  不过，如果您将站点搭建在 github repository 上，**任何非官方的插件都是不会被加载的**！

## **4 安装 DISQUS**

- DISQUS 支持将评论插件安装在各种不同的博客系统中，
  jekyll 可以通过添加 javascript 代码的方式来导入插件。
- 主要步骤：
  - ``1.`` 如果没有 DISQUS 账号，要先注册一个。
  - ``2.`` 登录 DISQUS 账号后，点击 Admin，点击 Installing Disqus, 选择平台(jekyll).
  - ``3.`` 按照说明文档将代码添加到你的 jekyll 项目中去。

