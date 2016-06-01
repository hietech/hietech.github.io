---
layout: post
title: 那么你想制作CSS3字体吗？
date: 2012-07-17 11:38
comments: true
categories: [front-end]
---

最近使用CSS3字体的项目发布了，在组里分享了一下相关流程。

如果没有读过之前我的@font-face实战，请移步：<a href="http://yuguo.us/weblog/font-face-in-action/">http://yuguo.us/weblog/font-face-in-action/</a>
为了讲清楚流程，我用PS很不职业地画了一个流程图。
<a href="http://yuguo.us/files/2012/07/font.png"><img class="aligncenter size-full wp-image-1275" title="font" src="http://yuguo.us/files/2012/07/font.png" alt=""   /></a>
所以问题是当我们制作一个全新字体库的时候，里面的图形都要我们从矢量设计稿中扒出来，这是一个相对比较人工的操作，而且是团队协作的时候比较容易起冲突的操作。

此外还有一个有意思的问题：如果我们做spirit image，图中可以合并的小图片书目理论上是无限的；那么我们在一个字体中包含的图标可以是多少种呢？

首先我们要了解编码和字形之间是没有必然联系的：
<blockquote>在文字处理方面，统一码为每一个字符而非字形定义唯一的代码（即一个整数）。换句话说，统一码以一种抽象的方式（即数字）来处理字符，并将视觉上的演绎工作（例如字体大小、外观形状、字体形态、文体等）留给其他软件来处理，例如网页浏览器或是文字处理器。</blockquote>
也就是说我完全可以做一个字体，对应字母A的编码的那个字形弄个B的样子，对应B的就弄个X，虽然很蛋疼，但是在机器看来是很正常的。（话说是有这样的密码的，正常人眼看上去就是乱码，只能根据字典来破解。不过现在计算机可以根据字频统计来反向破解出来。扯远了……）

那么我们有多少编码可以用？
<blockquote>目前，几乎所有电脑系统都支持<strong>基本拉丁字母</strong>，并各自支持不同的其他编码方式。Unicode为了和它们相互兼容，其<strong>首256字符</strong>保留给ISO 8859-1所定义的字符，使既有的<strong>西欧语系文字的转换不需特别考量</strong>；并且把大量相同的字符重复编到不同的字符码中去，使得旧有纷杂的编码方式得以和Unicode编码间互相直接转换，而不会遗失任何资讯。举例来说，<a title="全角" href="http://zh.wikipedia.org/wiki/%E5%85%A8%E5%BD%A2">全角</a>格式区段包含了主要的拉丁字母的全角格式，在中文、日文、以及韩文字形当中，这些字符以全角的方式来呈现，而不以常见的半角形式显示，这对竖排文字和等宽排列文字有重要作用。</blockquote>
简单的答案是：256个。

复杂的答案是：这要看你的字体是希望采用什么编码？你的网站面向多少种语言的用户？只有<a href="http://www.unicodetools.com/unicode/codepage-latin.php">基本拉丁字符</a>是所有计算机都支持的，其他字符比如中文系统和韩文系统是各自的系统才有的。如果做一个韩文编码的字体的话，那可以放上万种图标进去，但是在中文计算机上就会乱码。

所以如果256个是够用的，那就默认用编码的前256位即可。

为什么是256呢？二位的16进制能表示的字符数（从00到FF）是256个。

以字母A（大写）为例，它是第65个字符，对应的16进制编码是41（4*16+1=65），对应的拉丁字符是A。所以我们在网页上想输出A的时候，在源码中可以有以下几种选择：
<ul>
	<li>可以用键盘直接（Shift+a）</li>
	<li>可以用十进制编码&amp;#65;</li>
	<li>可以用十六进制&amp;#x41;</li></ul>
大概就是这样了，拥有了这些知识你就可以把基本拉丁字符的256个坑都设置对应的图标，然后使用以上的输入方法来输出到html中去。

如果你是个变态，希望使用更多的字符，那么可以考虑使用中文的<a href="http://www.wctutorials.com/reference/css/properties/unicode-range">unicode range</a>。然后<a href="http://stackoverflow.com/questions/1366068/whats-the-complete-range-for-chinese-characters-in-unicode">看看这个</a>。

