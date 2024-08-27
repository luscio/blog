---
title: 解决iframe出现滚动条
date: 2019/05/08 16:46
tags:
  - css
categories:
  - css
---

* 需求是这样的，iframe在一个div中，并且iframe高度与div一样，所以设置了iframe高度是100%，结果div出现了滚动条，在排除了padding、margin的因素外，还是有滚动条。按理说，只有iframe有滚动条，父div不应该有滚动条。  

* 一般搜索后，找到了原因，简单来说，iframe=inline frame它是一个内联元素，默认是跟baseline对齐的，iframe后边有个看不见、摸不着的行内空白节点，空白节点占据着高度，iframe与空白节点的基线对齐，导致了div被撑开，从而出现滚动条。

* 找到原因了，解决方案也就简单了。
    * 第一种，设置iframe的vertical-align:top，设置父div的font-size:0，从而影响空白节点的line-height是0，从而不占据高度
    * 第二种，改变iframe的内联元素性质，改为块级元素，display:block