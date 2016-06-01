---
layout: post
title: HTML5拖拽文件以及显示文件
date: 2011-03-16 10:21
comments: true
categories: [front-end]
---

利用支持HTML5（具体是拖拽API和File API）的浏览器拖拽图片/音频文件到浏览器窗口指定区域来看到预览（还未上传），需要了解的知识主要是拖拽API，和通过拖拽事件获得File之后，对File进行相关信息读取。在HTML5出现之前读取文件信息操作往往是通过后台来实现，现在浏览器也具有了这样的能力，就能提供更好的用户体验。需要的知识大概如下：
<ol>
	<li>(拖拽事件 API) 拖放文件到页面上的指定区域，<strong><a href="http://rebuildpattern.com/node/68">drop事件</a></strong>发生</li>
	<li>(拖拽事件 API) 从drop事件取得<strong><a href="http://rebuildpattern.com/node/64">DataTransfer</a></strong>对象</li>
	<li>(File API) 调用DataTransfer对象的files属性，得到<strong><a href="http://rebuildpattern.com/node/64">FileList</a></strong>，它代表了拖放文件的列表。</li>
	<li>(File API) 遍历FileList，得到每一个单独的<strong><a href="http://rebuildpattern.com/node/64">File对象</a></strong>。</li>
	<li>(File API) 通过<strong><a href="http://rebuildpattern.com/node/65">FileReader对象</a></strong>来读取每一个File对象的内容（FileReader.readAsDataURL(file)）。然后一个新的<strong><a href="http://rebuildpattern.com/node/69">data URI</a></strong>格式对象被创建，然后剩下的就交给onloadend回调函数来处理。</li>
	<li>(File API) 现在我们通过对拖拽文件的处理得到了一个“data URL”，比如显示图片和MP3播放器。或者可以通过读取<strong>text</strong>来获得拖拽css文件的文本内容。</li></ol>
