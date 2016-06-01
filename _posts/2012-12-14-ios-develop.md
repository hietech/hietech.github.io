---
layout: post
title: iOS开发随笔
date: 2012-12-14 10:27
comments: true
categories: [iOS]
---

随意记录一下一些经验，对新手可能有帮助。
<h2>数组NSArray</h2>
操作数组的时候计算数组包含的对象个数是：
<pre><code>[dataArray count]</code></pre>
获取索引处的对象
<pre><code>[dataArray objectAtIndex:2]</code></pre>
删除指定索引处对象
<pre><code>[dataArray removeObjectAtIndex:1];</code></pre><h2>词典NSDictionary</h2>
获取对应key的object：
<pre><code>- (id)objectForKey:(id)aKey</code></pre><h2>类方法和实例方法</h2>
在类方法中调用类方法
<pre><code>+ (void)classMethodB { </code></pre><pre><code>// ... </code></pre><pre><code>[self classMethodA]; </code></pre><pre><code>// ... </code></pre><pre><code>}</code></pre>
在实例方法中调用类方法
<pre><code>- (void)instanceMethodB { </code></pre><pre><code>// ...</code></pre><pre><code> [[self class] classMethodA];</code></pre><pre><code>// ...</code></pre><pre><code>}</code></pre><h2>NSLog</h2>
用NSLog记录debug数据，是一个很常用的方法。
<pre><code>NSLog(@"String"); NSLog(@"%@",someString); NSLog(@"%d",someInteger); NSLog(@"my float is %f",someFloat);</code></pre><h2>tag</h2>
在运行时获取某些视图可以用方法
<pre><code>- (UIView *)viewWithTag:(NSInteger)</code>tag</pre>
在storyboard中可以看到所有视图的默认tag都是0，可以改成特定的值，比如1。

如果要获得某个视图里的tag为某值的子视图，可以用这个自定义类方法
<pre><code>+(UIView*) getSubViewInViewWithTag:(UIView*)view withTag:(NSInteger)tag { for (UIView *subview in view.subviews) { if(subview.tag==tag) return subview; } return nil; }</code></pre><h2> indexPath转成整数？</h2>
在委托tableView或者collectionView的时候，需要实现的方法比如：
<pre><code>- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath</code></pre>
有一个参数是NSIndexPath，用来表示绘制第几个表格或者collectionCell，我需要得到它的整数值以便跟我自己的数据数组对应，方法很简单
<pre><code>indexPath.row</code></pre><h2>自己释放内存的图片</h2>
以下代码不会产生内存泄漏，因为这个newImage是一个自释放内存的图片。
<pre><code>UIImage *newImage = [UIImage imageNamed:@"sampleImage"]; [yourImageView setImage:newImage];</code></pre>
-imageNamed: returns an autoreleased image, which, as deanWombourne says, will be autoreleased at some time in the future (the exact time is undefined).

但是如果图片在其他地方生成，在这里使用，那么可能需要手动释放内存。

