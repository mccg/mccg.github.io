---
layout: post
title: "如何让搬砖更迅捷"
category: Dev
tags: ["copyq", "vim"]
date: 2018-03-30
comments: true

---

>**引言**:
复制粘贴各种代码已经是各路 coder 的家常便饭,
大家给了这种日常操作一种形象的比喻 ------ "搬砖".
本文将要介绍一款便捷的复制粘贴工具 ------ CopyQ.

## CopyQ
- CopyQ 是一款**免费**、[开源](https://github.com/hluk/CopyQ)、支持多种平台(Windows, MacOS 等)的粘贴板管理工具,
  有了它, 你可以方便地查找或者重新粘贴曾经拷贝过的文本或对象.
  特别是在批量性复制粘贴多段文本时, 它可以帮助你避免编辑窗口的切换或者是视图的频繁滚动.
- [下载](https://github.com/hluk/CopyQ/releases)安装并打开 CopyQ, 在全局快捷键设置中,
  可以方便地设置你认为趁手的快捷键, 最常用的操作应该就是 ``显示/隐藏主窗口`` 了.

## 自从有了 CopyQ
- vim 环境下的复制粘贴就轻松了许多.
  在命令行下 ``vim --version``, 如果看到有 +clipboard 选项,
  说明你的 vim 支持拷贝到粘贴版中!
  然后在 vim 中 ``:reg`` 可以看到 vim 粘贴板寄存器的内容,
  名称为 ``"*`` 的寄存器就保存着现在粘贴版的内容,
  使用 ``"*p``(Paste) 和 ``"*y``(Yank) 来和 clipboard 进行交互!
  现在可以使用 ``"*y`` 来把一部分搬砖寄存工作交给 CopyQ 来做了,
  毕竟 CopyQ 的可视化比 vim 好很多!

