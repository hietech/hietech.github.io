---
layout: post
title: 字体是个深坑
date: 2012-07-20 17:27
comments: true
categories: [front-end]
---
<a href="http://yuguo.us/files/2012/07/2.png"><img class="aligncenter size-full wp-image-1282" title="2" src="http://yuguo.us/files/2012/07/2.png" alt=""   /></a>
如图，左边是12号的Arial字体，右边是12号的宋体，为啥他们一个有边缘半透明一个没有呢？
<a href="http://yuguo.us/files/2012/07/3.png"><img class="aligncenter size-full wp-image-1283" title="3" src="http://yuguo.us/files/2012/07/3.png" alt=""   /></a>
如图，上面的是Chrome下的48号图标字体，下图是49号，为啥下面的明显比上面平滑呢？
<a href="http://yuguo.us/files/2012/07/4.png"><img class="aligncenter size-full wp-image-1284" title="4" src="http://yuguo.us/files/2012/07/4.png" alt=""   /></a>
如图，IE渲染图标的时候为什么垂直方向比水平方向更平滑呢？

有什么CSS属性可以让字体变得平滑呢？

当我脑中浮现出这些问题的时候，辣就是一个深坑啊有木有！两个小时查了80+个英文站，结论如下：
<h2>outline和bitmap</h2>
简单的说，字体格式分三类其中两大类分别是outline的和bitmap的，就是矢量和点位图。点位图字体是常用语Linux系统的一种老式字体，对于每个固定的font-size都会储存每一个文字的点位图片。矢量字体就是常用的opentype和truetype之类了，字体储存的是矢量信息，所以字体设置不同的font-size的时候都可以缩放。
<h2>outline字体可以内嵌bitmap</h2>
The <code>'EBSC'</code> table provides a mechanism for forcing the TrueType scaler to use a particular size of embedded bitmap when generating glyphs for a different point size.

这样一个truetype的字体.ttf也能包含bitmap，宋体就是这么干的，宋体中包含了12、13、14、15、16、17等字号的点位图，而其他字号的时候，会使用宋体的outline来渲染。
<h2>Chrome</h2>
字体的具体渲染还是由浏览器来实现，Chrome跟IE在这一点上是不同的，Chrome在渲染小于48px的字体的时候有明显锯齿，大于等于49px的时候就变平滑了。而IE在渲染的时候垂直方向比水平方向更平滑。
<h2>Font-smooth/text-shadow</h2>
stackoverflow上有人问了能不能用CSS属性让字体变得平滑，结论有两个，一个是font-smooth（现在只有-webkit-font-smoothing在mac下实现了这一效果，Windows下能识别这一属性，但并不影响渲染），另一个是text-shadow，用在某些文字font下还有效果，但在图标应用上，效果不大。
<h2>结论</h2>
图标字体很模糊，没啥解决办法。

好，下面是参考资料：
<a href="http://en.wikipedia.org/wiki/Computer_font">Computer font</a> （告诉你outline字体和bitmap字体的区别）

<a href="http://www.differencebetween.net/technology/difference-between-opentype-and-truetype/">Difference Between Opentype and Truetype</a> （这个可以跳过）

<a href="https://developer.apple.com/fonts/ttrefman/rm06/Chap6EBSC.html">The <code>'EBSC'</code> table</a> （原来outline是可以内嵌bitmap——embeded bitmap）

<a href="http://fontforge.sourceforge.net/editexample8.html">Opening &amp; Importing Bitmap strikes</a> （可以使用fontforge制作内嵌bitmap的opentype和truetype）

<a title="Permanent Link to Font anti-aliasing technique in Chrome changes after 48px size" href="http://inodetelic.com/random/font-anti-aliasing-technique-in-chrome-changes-after-48px-size/" rel="bookmark">Font anti-aliasing technique in Chrome changes after 48px size</a> （坑爹，Chrome的字号大于48的时候突然变得平滑了，好吧经过我的测试，大于393px的时候也是会突然变模糊）

<a href="http://stackoverflow.com/questions/3451541/css-font-face-anti-aliasing">CSS: @font-face anti aliasing</a> （对于icon字体 ，都没效果）

<a title="Permanent Link: mac下网页中文字体优化" href="http://www.qianduan.net/mac-the-next-pages-of-chinese-fonts-optimized.html" rel="bookmark">mac下网页中文字体优化</a> （font-smooth只有mac下才有效果……）
