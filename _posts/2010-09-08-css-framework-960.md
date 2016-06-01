---
layout: post
title: css框架[3]-960grids
date: 2010-09-08 20:02
comments: true
categories: [front-end]
---

960grids是一个欢乐的框架，极端理性+方便+易于维护，同时极端冗余，适用于设计师使用。

960grids框架是基于栅格理论而建立的，射雕前辈的两篇日志《[网页栅格系统研究（1）：960的秘密](http://lifesinger.org/blog/2008/10/grid-system-1/)》和《[网页栅格系统研究（2）：蛋糕的切法](http://lifesinger.org/blog/2008/10/grid-system-2/)》详细地介绍了960像素是怎么来的，950像素又是怎么回事。

由于我负责的项目不是基于栅格的，所以对我来说就无法把它应用在项目中。

真正吸引我的有这样3点：

1.960grids不仅提供HTM和css代码，还提供了Acorn, Fireworks, Flash, InDesign, GIMP, Inkscape, Illustrator, OmniGraffle, Photoshop, Visio, Exp Design. Also: PDF sketch sheets + CSS files.这一大坨我都不知道是什么的周边工具。_因为它是严格基于栅格的，所以也能够做出这样的衍生物来_，这是它跟之前介绍的oocss和YUI最大的区别。

2._960grids提供了一个自动工具来生成表格_，我试了一下，非常方便，并且灵活性也明显比YUI的自动工具高。在HTML5和CSS3盛行的今天，未来的框架或者标准、模块可能都会提供类似的web APP。如果项目有自己的标准和模块，那么自己做一个类似的工具集，设计和技术都可以参考这些优秀的自动工具。

3.一个在页面上蒙上栅格的[书签](http://gridder.andreehansson.se/)，以此来测试当前页面是否符合栅格。不过这个工具不太灵活，默认显示960像素，也无法设定margin。我有一个更好的[书签工具](http://www.sprymedia.co.uk/article/Design)，并且不仅有显示栅格的功能，还有几种规格的尺子。

[![960grids的代码生成工具](http://yuguo.us/files/2010/09/2010-9-8-17-32-50-copy.png "960grids的代码生成工具")](http://yuguo.us/files/2010/09/2010-9-8-17-32-50-copy.png)