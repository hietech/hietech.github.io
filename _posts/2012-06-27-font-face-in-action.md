---
layout: post
title: font-face实战
date: 2012-06-27 17:29
comments: true
categories: [front-end]
---

以前都只是理论，最近我在Qzone真正开始使用字体来实现图标。

如果以前都不了解这一话题，可以先看看<a href="https://twitter.com/#!/mienflying">@shenfei</a>的两篇超赞文章：<a href="http://www.qianduan.net/css3-icon-font-guide.html">《CSS3 icon font完全指南》</a>和<a href="http://www.qianduan.net/icon-font-large-collecting.html">《icon font大搜罗》</a>。

与一些CSS3的渐进增强不一样，使用字体来实现图标是跨浏览器兼容的，甚至IE6都完美兼容。当然，需要在代码和字体文件上下一些功夫。

介绍一下我在实际项目中使用web font的心得吧，作为@shenfei的两篇文章的补充，<strong>优点是</strong>：
<ul>
	<li>所有可以设置在文字上的CSS属性都可以设置在icon font上，比如color、font-size、text-shadow等</li>
	<li>由于是网页读取矢量字体，无论放大到多少倍都比较清晰，不会像jpg/png图片那样模糊</li>
	<li>不用为IE6单独点实一个png8，而为其他浏览器提供带alpha的png。比较方便。</li></ul><strong>缺点是</strong>：
<ul>
	<li>太太太麻烦，在自定义的字体库中增加一个文字（也就是图标）需要开AI、Fontgrapher（或者其他软件），完了生成的ttf还需要找一个网上的互转工具转化成兼容其余浏览器的字体 <a href="http://www.fontsquirrel.com/fontface/generator">Font Squirrel | Create Your Own @font-face Kits</a></li>
	<li>如果多人协作的话，不方便系统管理。而雪碧图使用CSSgaga来自动合并是很好多人协作的。</li>
	<li>Chrome等浏览器对文字的解析还是不够平滑，边缘有小锯齿。</li></ul><strong>结论</strong>：
<ul>
	<li>如果你的网站是配色可变的，并且图标也要随着配色的修改改变颜色（不会吧，这个世界上应该只有QZone是这样的），那么使用web font是一个很好的选择，或者说唯一的技术选择；</li>
	<li>如果你要快速做一个小站，并且有开源的icon font库，那么直接用吧！</li>
	<li>如果你想自己把设计稿中的图标都做成icon font，请三思 ，会有不小的制作成本、维护成本。</li></ul>
开发人员的制作成本和维护成本是我认为在大型项目中要考虑的最重要的成本之一，除非跟其他考虑的点比如性能有巨大的冲突，否则都应该考虑这一成本。

前端开发永远是关于平衡的博弈。

update：

遇到了唯一一个兼容性问题就是FF在iframe里不会载入我的自定义字体。

查了这个：<a href="http://stackoverflow.com/questions/5128202/fonts-not-showing-up-in-iframe-in-firefox">http://stackoverflow.com/questions/5128202/fonts-not-showing-up-in-iframe-in-firefox</a> 说是FF有一个跨域政策，如果字体文件的http头中没有指明Access-Control-Allow-Orig这个属性的话，那就不会加载这个字体，是为了防止盗用字体。

解决方法：<a href="http://www.cssbakery.com/2010/07/fixing-firefox-font-face-cross-domain_25.html">http://www.cssbakery.com/2010/07/fixing-firefox-font-face-cross-domain_25.html</a>
所以要要改Apache设置才能实现字体跨域。

