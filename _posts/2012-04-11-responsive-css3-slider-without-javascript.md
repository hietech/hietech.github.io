---
layout: post
title: 实现纯CSS3幻灯片的一种思路
date: 2012-04-11 01:59
comments: true
categories: [front-end]
---

今天看到一个有意思的demo，用纯css3实现了幻灯片。
<a href="http://csscience.com/responsiveslidercss3/">http://csscience.com/responsiveslidercss3/</a>
Best In Test: Firefox (transition performance)

Full Support: Chrome, Firefox, Opera, Safari (latest versions of all browsers)

Partial Support: IE9 (Functional, but does not support transitions)
<pre><a href="http://yuguo.us/files/2012/04/1.jpg"><img title="1" src="http://yuguo.us/files/2012/04/1.jpg" alt=""   data-pinit="registered" /></a></pre><h2>幻灯片</h2>
所有的幻灯片&lt;article&gt;挨着浮动在一起，然后放到一个大容器#slides #overflow #inner中。大容器通过#overflow溢出隐藏。当点击左右的滑动箭头的时候，对#inner设置left-margin: -100%;就会让所有幻灯片滑到左边。

这一点跟普通的js幻灯片没有什么两样。

不同的是所有箭头并非触发js动作，而是通过label和select来实现动作的关联。

页面中有5个label和5个select。左右两个箭头是对应其中两个label，点击之后会使label对应的select选中。

select选中之后就会通过CSS3来触发margin的改变。
<pre>#slide1:checked ~ #slides .inner { margin-left:0; }

#slide2:checked ~ #slides .inner { margin-left:-100%; }

#slide3:checked ~ #slides .inner { margin-left:-200%; }

#slide4:checked ~ #slides .inner { margin-left:-300%; }

#slide5:checked ~ #slides .inner { margin-left:-400%; }</pre>
然后同时改变label的显示和隐藏，也就是替换成其他的label。
<pre>#slide1:checked ~ #controls label:nth-child(2),

#slide2:checked ~ #controls label:nth-child(3),

#slide3:checked ~ #controls label:nth-child(4),

#slide4:checked ~ #controls label:nth-child(5),

#slide5:checked ~ #controls label:nth-child(1) {

	background: url('next.png') no-repeat;

	float: right;

	margin: 0 -70px 0 0;

	display: block;

}/*右边的label，控制下一张幻灯片，所以当#slide1是当前幻灯片的时候，下一张幻灯片是第二个label，也就是#slide2，实现了切换*/

#slide1:checked ~ #controls label:nth-child(5),

#slide2:checked ~ #controls label:nth-child(1),

#slide3:checked ~ #controls label:nth-child(2),

#slide4:checked ~ #controls label:nth-child(3),

#slide5:checked ~ #controls label:nth-child(4) {

	background: url('prev.png') no-repeat;

	float: left;

	margin: 0 0 0 -70px;

	display: block;

}</pre>
此外还有幻灯片上的文字信息的隐现：
<pre>#slide1:checked ~ #slides article:nth-child(1) .info,

#slide2:checked ~ #slides article:nth-child(2) .info,

#slide3:checked ~ #slides article:nth-child(3) .info,

#slide4:checked ~ #slides article:nth-child(4) .info,

#slide5:checked ~ #slides article:nth-child(5) .info {

	opacity: 1;

	-webkit-transition: all 1s ease-out 0.6s;

	-moz-transition: all 1s ease-out 0.6s;

	-o-transition: all 1s ease-out 0.6s;

	transition: all 1s ease-out 0.6s;

}</pre>
这样就会出现幻灯片快速滑动之后，文字慢慢隐现出来的感觉。
<h2>Responsive Design</h2>
在国外很多前卫网站设计中，Responsive Design几乎成了标配（<a href="http://yuguo.us/weblog/">yuguo.us/weblog</a>也是），在这个幻灯片中通过@media标签把显示媒介分为桌面、平板电脑和手机三类。

主要做了这样一些工作：
<ol>
	<li>label图标缩小
<pre>#tablet:checked ~ #slider #controls label {

-moz-transform: scale(0.8);

-webkit-transform: scale(0.8);

-o-transform: scale(0.8);

-ms-transform: scale(0.8)

transform: scale(0.8);

}</pre></li>
	<li>label图标移到幻灯片内容中</li>
	<li>其他样式修饰，比如去掉圆角</li></ol>
