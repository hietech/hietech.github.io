---
layout: post
title: 15条JavaScript最佳实践
date: 2013-01-03 01:05
comments: true
categories: [front-end]
---
<p>本文档整理大部分公认的、或者少有争议的JavaScript良好书写规范（Best Practice）。一些显而易见的常识就不再论述（比如要用对象支持识别判断，而不是浏览器识别判断；比如不要嵌套太深）。条目顺序按重要级粗略的从高到低排列。</p><h2 id="js-at-bottom">把外部JavaScript文件放在HTML底部</h2><p>我们的目标是相同的：为用户尽可能快地显示内容。当载入一个脚本文件的时候，HTML会停止解析，直到脚本载入完毕。因此，用户可能会长时间对着一个空白的屏幕，看上去什么都没有发生。如果你的JavaScript代码只是增加一些功能（比如按钮的点击动作），那么尽管大胆地把文件引用放在HTML底部吧（就在&lt;/body&gt;之前），你会看到明显的速度提升。如果是用于其他目的的脚本文件，则需要慎重地考虑。但无论如何，这毫无疑问是一个非常值得考虑的地方。</p><h2 id="optimize-for-statement">优化循环</h2><p>循环遍历一个数组</p><pre class="badcode">//这段糟糕的代码会在每次进入循环的时候都计算一次数组的长度

var names = ['George','Ringo','Paul','John'];

for(var i=0;i&lt;names.length;i++){

  doSomeThingWith(names[i]);

}
</pre><pre class="goodcode">//这样的话，就只会计算一次了

var names = ['George','Ringo','Paul','John'];

var all = names.length;

for(var i=0;i&lt;all;i++){

  doSomeThingWith(names[i]);

}
</pre><pre class="goodcode">//这样就更加简短了

var names = ['George','Ringo','Paul','John'];

for(var i=0,j=names.length;i&lt;j;i++){

  doSomeThingWith(names[i]);

}
</pre><pre class="badcode">//这段代码的糟糕之处在于，它把变量声明放在循环体内了，每次循环都会创建变量

for(var i = 0; i &lt; someArray.length; i++) {

   var container = document.getElementById('container');

   container.innerHtml += 'my number: ' + i;

   console.log(i);

}
</pre><pre class="goodcode">//在循环体外声明变量，变量只会创建一次

var container = document.getElementById('container');

for(var i = 0, len = someArray.length; i &lt; len;  i++) {

   container.innerHtml += 'my number: ' + i;

   console.log(i);

}
</pre><h2 id="shortcut-notation">用尽量简短的代码</h2><p>如果可以增加可读性的话，那么使用代码的简短格式是有意义的，下面是一份不完全的列表：</p><pre class="badcode">//对于条件判断只有两次的，这是一种冗长的写法

var direction;

if(x &gt; 100){

  direction = 1;

} else {

  direction = -1;

}
</pre><pre class="goodcode">//更好的代码

var direction = (x &gt; 100) ? 1 : -1;
</pre><pre class="badcode">//判断一个 变量是否定义，如果否，就赋予一个值，糟糕的代码

if(v){

  var x = v;

} else {

  var x = 10;

}
</pre><pre class="goodcode">//更好的代码

var x = v || 10;
</pre><pre class="badcode">//重复了变量名很多次

var cow = new Object();

cow.colour = 'brown';

cow.commonQuestion = 'What now?';

cow.moo = function(){

  console.log('moo');

}

cow.feet = 4;

cow.accordingToLarson = 'will take over the world';
</pre><pre class="goodcode">//更好的写法是这样

var cow = {

  colour:'brown',

  commonQuestion:'What now?',

  moo:function(){

    console.log('moo);

  },

  feet:4,

  accordingToLarson:'will take over the world'

};
</pre><pre class="badcode">//重复了很多次数组名

var aweSomeBands = new Array();

aweSomeBands[0] = 'Bad Religion';

aweSomeBands[1] = 'Dropkick Murphys';

aweSomeBands[2] = 'Flogging Molly';

aweSomeBands[3] = 'Red Hot Chili Peppers';

aweSomeBands[4] = 'Pornophonique';
</pre><pre class="goodcode">//更好的代码

var aweSomeBands = [

  'Bad Religion',

  'Dropkick Murphys',

  'Flogging Molly',

  'Red Hot Chili Peppers',

  'Pornophonique'

];
</pre><h2 id="quotes">单引号和双引号</h2><p>为了避免混乱，我们建议在HTML中使用双引号，在JavaScript中使用单引号。</p><pre class="goodcode">//html

&lt;img src="picture.gif" /&gt;
</pre><pre class="goodcode">//JavaScript

&lt;script type="text/javascript"&gt;

document.write('&lt;p&gt;');

&lt;/script&gt;
</pre><pre class="goodcode">//一段混用的jQuery代码

$('h1').after('&lt;div id="content"&gt;&lt;h2&gt;目录&lt;/h2&gt;&lt;ol&gt;&lt;/ol&gt;&lt;/div&gt;');
</pre><h2 id="avoid-other-tech">避免混入其他技术</h2><p>CSS:假设我们的页面上有必须填入的输入框（拥有class“mandatory”），如果它没有被输入数据，周围就会加上红色边框。</p><pre class="badcode">//一段混合了其他技术的代码会这样做：

var f = document.getElementById('mainform');

var inputs = f.getElementsByTagName('input');

for(var i=0,j=inputs.length;i&lt;j;i++){

  if(inputs[i].className === 'mandatory' &amp;&amp;

     inputs[i].value === ''){

    inputs[i].style.borderColor = '#f00';

    inputs[i].style.borderStyle = 'solid';

    inputs[i].style.borderWidth = '1px';

  }

}
</pre><pre class="goodcode">//一段良好的代码会这么做：将风格化的事情交给CSS吧

var f = document.getElementById('mainform');

var inputs = f.getElementsByTagName('input');

for(var i=0,j=inputs.length;i&lt;j;i++){

  if(inputs[i].className === 'mandatory' &amp;&amp;

     inputs[i].value === ''){

    inputs[i].className += ' error';

  }

}
</pre><p>HTML:假设我们有内多HTML内容需要用JavaScript来载入，那么使用Ajax载入单独的文件，而不是通过JavaScript处理DOM，后者会让代码难以处理，并且出现难以维护的兼容性问题。</p><h2 id="strict-js">验证JavaScript代码</h2><p>浏览器处理JavaScript代码可能会非常宽容，但我建议你不要依赖浏览器的解析能力，因此养成了懒散的编码习惯。</p><p>最简单的检测你的代码质量的方法是通过一个在线JavaScript验证工具<a href="http://www.jslint.com/">JSLint</a>。</p><p>“JSLint takes a JavaScript source and scans it. If it finds a problem, it returns a message describing the problem and an approximate location within the source. The problem is not necessarily a syntax error, although it often is. JSLint looks at some style conventions as well as structural problems. It does not prove that your program is correct. It just provides another set of eyes to help spot problems.”<br />
– JSLint Documentation</p><h2 id="simple-javascript">使用更简单的格式来写innerscript</h2><pre class="badcode">//早期的代码可能是这样的

&lt;script type="text/javascript" language="javascript"&gt;

...

&lt;/script&gt;
</pre><pre class="goodcode">//现在不用language属性了

&lt;script type="text/javascript"&gt;

...

&lt;/script&gt;
</pre><h2 id="check-data">总是检查数据</h2><p>要检查你的方法输入的所有数据，一方面是为了安全性，另一方面也是为了可用性。用户随时随地都会输入错误的数据。这不是因为他们蠢，而是因为他们很忙，并且思考的方式跟你不同。用typeof方法来检测你的function接受的输入是否合法。</p><pre class="badcode">//如果members的类型不是数组，那么下面的代码会抛出一个错误

function buildMemberList(members){

  var all = members.length;

  var ul = document.createElement('ul');

  for(var i=0;i</pre><pre class="goodcode">//良好的习惯是检查参数是否是一个数组

function buildMemberList(members){

//数组的typeof是object，所以如果要判断是否为数组的话，可以测试它是否拥有数组才有的function：slice

  if(typeof members === 'object' &amp;&amp;

     typeof members.slice === 'function'){

    var all = members.length;

    var ul = document.createElement('ul');

    for(var i=0;i</pre><p>另一个安全隐患是直接从DOM中取出数据使用。比如说你的function从用户名输入框中取得用户名做某项操作，但用户名中的单引号或者双引号可能会导致你的代码崩溃。</p><h2 id="avoid-global">避免全局变量</h2><p>全局变量和全局函数是非常糟糕的。因为在一个页面中包含的所有JavaScript都在同一个域中运行。所以如果你的代码中声明了全局变量或者全局函数的话，后面的代码中载入的脚本文件中的同名变量和函数会覆盖掉（overwrite）你的。</p><pre class="badcode">//糟糕的全局变量和全局函数

var current = null;

function init(){...}

function change(){...}

function verify(){...}
</pre><p>解决办法有很多，<a href="http://dev.opera.com/author/1037557">Christian Heilmann</a>建议的方法是：</p><pre class="goodcode">//如果变量和函数不需要在“外面”引用，那么就可以使用一个没有名字的方法将他们全都包起来。

(function(){

  var current = null;

  function init(){...}

  function change(){...}

  function verify(){...}

})();
</pre><pre class="goodcode">//如果变量和函数需要在“外面”引用，需要把你的变量和函数放在一个“命名空间”中

//我们这里用一个function做命名空间而不是一个var，因为在前者中声明function更简单，而且能保护隐私数据

myNameSpace = function(){

  var current = null;

  function init(){...}

  function change(){...}

  function verify(){...}

  //所有需要在命名空间外调用的函数和属性都要写在return里面

  return{

    init:init,

    //甚至你可以为函数和属性命名一个别名

    set:change

  }

}();
</pre><h2 id="use-var">声明变量的话，总是用var</h2><p>JavaScript中的变量可能是全局域或者局部域，用var声明的话会更加直观。</p><pre class="badcode">//在function中不用var引起的迷惑性问题

var i=0; // This is good - creates a global variable

function test() {

  	 for (i=0; i&lt;10; i++) {

      	alert("Hello World!");

  	 }

}

test();

alert(i); // The global variable i is now 10!
</pre><pre class="goodcode">//解决方法是在function中声明变量也用var

function test() {

  	 for (var i=0; i&lt;10; i++) {

      	alert("Hello World!");

  	 }

}
</pre><h2 id="string-to-num">使用前置+号来把字符串转化为数字</h2><p>JavaScript中，“+”操作符即被用来作为数字加，也被用来连接字符串。如果需要求表单中几个值的和，那么用+可能会出现问题。</p><pre class="badcode">//会出现问题的代码

&lt;form name="myform" action="[url]"&gt;

&lt;input type="text" name="val1" value="1"&gt;

&lt;input type="text" name="val2" value="2"&gt;

&lt;/form&gt;

function total() {

	var theform = document.forms["myform"];

	var total = theform.elements["val1"].value + theform.elements["val2"].value;

	alert(total); // This will alert "12", but what you wanted was 3!

}
</pre><pre class="goodcode">//在字符串前面加上“+”，这是给JavaScript的一个暗示：这是一个数字而不是字符串

function total() {

	var theform = document.forms["myform"];

	var total = (+theform.elements["val1"].value) + (+theform.elements["val2"].value);

	alert(total); // This will alert 3

}
</pre><h2 id="avoid-eval">避免使用eval()方法</h2><p>JavaScript中的eval()方法是在运行时把任何代码当作对象来计算/运行的方法。实际上由于安全性的缘故，大部分情况下都不应该用eval()，总是有一种更“正确”的方法来完成同样的工作的。基本原则是，eval is evil，在任何时候都不要用它，除非你是一个老手，并且知道你不得不这样做。</p><h2 id="for-in">for in语句</h2><p>遍历一个对象中的所有条目的时候，用for in语句是非常方便的。但有时候我们不需要遍历对象中的方法，如果不需要的话，可以加上一条filter。</p><pre class="goodcode">//加上了一个过滤器的for in语句

for(key in object) {

   if(object.hasOwnProperty(key) {

      ...then do something...

   }

}
</pre><h2 id="no-shot-hand">不要偷懒省略”和{}</h2><p>从技术上说，你可以忽略很多花括号和分号。</p><pre class="badcode">//虽然看上去很不对头，大部分浏览器都能正确解析这段代码

if(someVariableExists)

  x = false
</pre><pre class="badcode">//这个代码看上去更不对头了，咋眼一看似乎下面的句都被执行了

//实际上只有x=false在if中

if(someVariableExists)

   x = false

   anotherFunctionCall();
</pre><p>所以，要记住的原则是：1.永远不要省略分号；2.不要省略花括号，除非在同一行中。</p><pre class="goodcode">//这样是OK的

if(2 + 2 === 4) return 'nicely done';
</pre><h2 id="use-square-bracket">获取对象属性的时候用方括号而不是点号</h2><p>在JavaScript中取得某对象的属性有两种方法：</p><pre class="goodcode">//点号标记

MyObject.property
</pre><pre class="goodcode">//方括号标记

MyObject["property"]
</pre><p>如果是用点号标记取得对象的属性，属性名称是硬编码，无法在运行时更改；而用方括号的话，JavaScript会求得方括号内值然后通过计算结果来求得属性名。也就是说用方括号标记的方式，属性名称可以是硬编码的，也可以是变量或者函数返回值。</p><pre class="badcode">//这样是不行的

MyObject.value+i
</pre><pre class="goodcode">//这样就没有问题

MyObject["value"+i]
</pre><h2 id="enhance-progressively">假设JavaScript会被禁用</h2><p>我知道这样的假设会伤害JavaScript开发者的感情，可是在目前数据不明朗的情况下我们为了安全起见应该做这样的假设。这是渐进增强中很重要的一部分。</p><h2 id="use-library">使用JavaScript库</h2><p>现在有很多非常流行的JavaScript库，比如YUI和jQuery、Dojo。它们的缺点是需要下载一个额外的文件，优点却更多：兼容性更强；代码更简单易懂。好的库有很多，但你不应该在一个项目中把它们都用上，因为可能存在兼容性问题。选择一个自己习惯的就好。</p><p>不要忘记的一点是，原生的JavaScript毫无疑问更快，如果是小规模的使用，最好还是用原生的。</p>
