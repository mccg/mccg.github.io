---
layout: post
title: "如何在 Web 页支持数学符号"
category: Dev
tags: ["javascript", "jekyll", "web"]
date: 2017-08-26
---

>**引言**:
如果想要写一篇带有数学表达式的文章，页面能支持数学公式的话就再好不过了。
所以根据 jekyll 的官方文档找到了一个专门渲染数学符号的 `javascript` 库 --- MathJax.

## Getting Started
 - MathJax 的文档地址：[mathjax-getting-started](http://docs.mathjax.org/en/latest/start.html#getting-started)
 - 将下面的代码加入到`<head>`中去，样就可以在`<body>`中按照 MathJax 的符号写入数学公式了。
 - ```html
   <script type="text/javascript" async
   src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML">
   </script>
   ```

 - > 按照文档中的说明，javascript 库的地址可以在 [cdnjs.com](https://cdnjs.com) 查询得到。

## 数学公式


- ### 行内嵌入
  - 在 Tex／LaTex 中，行内嵌入的公式的符号是 `$ ...  $`,
    但是 MathJax 为了避免在一行之中出现两次 `$` 带来错误的解析结果,
    所以 `$ ... $` 是默认不解析的，
    开启解析需要进行[额外的配置](http://docs.mathjax.org/en/latest/start.html#tex-and-latex-input).
  - 简单的例子： $a^2 + b^2 = c^2$

- ### 稍微复杂的例子

  - | 代码                                               | 结果                                   |
    | ---                                                |:---:                                   |
    | `$x=\frac{1+y}{1+2z^2}$`                           |$x=\frac{1+y}{1+2z^2}$
    | `$\int_0^\infty e^{-x^2} dx=\frac{\sqrt{\pi}}{2}$` |$\int_0^\infty e^{-x^2} dx=\frac{\sqrt{\pi}}{2}$

- ### 更加复杂的例子
  - #### 例1
    - 代码：
      ```latex
      $$
      \frac{1}{\displaystyle 1+
         \frac{1}{\displaystyle 2+
         \frac{1}{\displaystyle 3+x}}} +
       \frac{1}{1+\frac{1}{2+\frac{1}{3+x}}}
      $$
      ```
    - 结果：
      $$
      \frac{1}{\displaystyle 1+
         \frac{1}{\displaystyle 2+
         \frac{1}{\displaystyle 3+x}}} +
       \frac{1}{1+\frac{1}{2+\frac{1}{3+x}}}
      $$

  - #### 例2
    - 代码：
      ```latex
      $$
      F(x,y)=0 ~~\mbox{and}~~
      \left| \begin{array}{ccc}
        F''_{xx} & F''_{xy} &  F'_x \\
        F''_{yx} & F''_{yy} &  F'_y \\
        F'_x     & F'_y     & 0
        \end{array}\right| = 0
      $$
      ```
    - 结果：
      $$
      F(x,y)=0 ~~\mbox{and}~~
      \left| \begin{array}{ccc}
        F''_{xx} & F''_{xy} &  F'_x \\
        F''_{yx} & F''_{yy} &  F'_y \\
        F'_x     & F'_y     & 0
        \end{array}\right| = 0
      $$
- > latex语法[参考](http://www.personal.ceu.hu/tex/cookbook.html)
