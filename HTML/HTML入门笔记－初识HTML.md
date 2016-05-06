本人在慕课网学习[HTML+CSS基础课程](http://www.imooc.com/learn/9)，记录一些文字，方便自己回忆，也希望对大家有所帮助

---
## **基础框架**
```
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>标题标签</title>
</head>
<body>
    <h1>了不起的盖茨比</h1>
    <p>《了不起的盖茨比》为那个奢靡年代的缩影。盖茨比怀揣着对"美国梦"的期翼，投身到那个年代的灯红酒绿之中，却在名利场中看尽世态炎凉，以及浮华背后一切终将逝去的空虚怅惘。1925年《了不起的盖茨比》问世。
    </p>
</body>
</html>
```
---
## **了解HTML的代码注释**
什么是代码注释？代码注释的作用是帮助程序员标注代码的用途，过一段时间后再看你所编写的代码，就能很快想起这段代码的用途。代码注释不仅方便程序员自己回忆起以前代码的用途，还可以帮助其他程序员很快的读懂你的程序的功能，方便多人合作开发网页代码。   

语法：
`<!--注释文字 -->`
---
## **认识标签`<head>`**
文档的头部描述了文档的各种属性和信息，包括文档的标题等。绝大多数文档头部包含的数据都不会真正作为内容显示给读者。  
```
<head>
    <title>...</title>
    <meta>
    <link>
    <style>...</style>
    <script>...</script>
</head>
```

1. `<title>`标签  
在`<title>` 和`<title>` 标签之间的文字内容是网页的标题信息，它会出现在浏览器的标题栏中。网页的title标签用于告诉用户和搜索引擎这个网页的主要内容是什么，搜索引擎可以通过网页标题，迅速的判断出网页的主题。每个网页的内容都是不同的，每个网页都应该有一个独一无二的title。  
例如：
```
<head>
    <title>hello world</title>
</head>
```
`<title>`标签的内容“hello world”会在浏览器中的标题栏上显示出来，如下图所示   
![](http://upload-images.jianshu.io/upload_images/1408656-2543f4a7f84fbdec.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
2. 页面关键字  
基本语法：	`<meta name="keywords" content="输入具体的关键字"> `  
举例：    	`<meta name="keywords" content="网页，学习">`  
3. 页面描述    
基本语法：`<meta name="description" content="设置页面描述"> `  
举例：`<meta name=“description” content="这是为了学习而建的网站">`  
4. 作者信息   
基本语法：`<meta name="author" content="作者的姓名"> `  
举例：`<meta name="author" content="***">`  
5. 网页到期时间  
基本语法：`<meta http-equiv="expires" content="过期时间">`   
举例：`<meta http-equiv="expires" content="31 Dec 2018 24:00:00 GMT">`    
说明: 必须使用GMT时间格式!
6. 禁止读缓存调阅页面内容   
当用户希望访问者每次访问都刷新网页广告的图标或每次都刷 新网页的计数器，就要禁用缓存了。  
基本语法：`<meta http-equiv="pragma" content="no-cache"> `  
7. 设置cookie过期  
基本语法：`<meta http-equiv="set-cookie" content=“过期时间">`    
举例：`<meta http-equiv=“set-cookie” content="31 Dec 2016 24:00:00 GMT">`  
说明: 必须使用GMT时间格式!  
8. 强制以独立页面打开  
基本语法：`<meta http-equiv="window-target" content="_top">`    
9. 定义网页文字及语言   
基本语法：`<meta http-equiv="content-type" content="text/html; charset=字符集类型">`   
举例：`<meta http-equiv="content-type" content="text/html; charset=utf-8">`     
10. 定义网页的定时跳转  
基本语法：`<meta http-equiv="refresh" content="跳转的时间;URL=跳转到的地址">`   
举例：`<meta http-equiv="refresh" content="5;URL=http://www.google.com">`   
11. 网页打开时或退出时的效果  
基本语法：`<meta http-equiv="page-exit" content="revealtrans(duration=延迟时间(秒),transition=数字 (转换方式))">`    
   &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;	&ensp;	  `<meta http-equiv="page-enter" content="revealtrans(duration=延迟时间(秒),transition=数字 (转换方式))">`  
举例：`<meta http-equiv="page-exit" content="revealtrans(duration=10,transition=21)">`   
 &ensp;&ensp;&ensp;&ensp; &ensp;  `<meta http-equiv="page-enter" content="revealtrans(duration=8,transition=12)">`   

|效果|transition|效果|transition|
|---|---|---|---|
|盒状收缩| 0| 溶解| 12|
|盒装展开|1 |左右向中部收缩| 13 |
|圆形收缩|2 |中部向左右展开 |14 |
|圆形展开| 3 |上下向中部收缩| 15|
|向上擦除| 4 |中部向上下展开| 16|
|向下擦除| 5 |阶梯状向左下展开| 17 |
|向左擦除 |6 |阶梯状向左上展开| 18|
|向右擦除 |7 |阶梯状向右下展开| 19|
|垂直百叶窗| 8| 阶梯状向右上展开| 20|
|水平百叶窗| 9| 随即水平线 |21 |
|横向棋盘式| 10 |随即垂直线 |22|
|纵向棋盘式| 11 |随即 |23|  
---
## **`<body>`标签，网页上显示的内容放在这里**
在网页上要展示出来的页面内容一定要放在body标签中。如下图是一个新闻文章的网页。
![](http://upload-images.jianshu.io/upload_images/1408656-c9cd44935f6c5044.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
## **开始学习`<p>`标签，添加段落**

如果想在网页上显示文章，这时就需要`<p>`标签了，把文章的段落放到`<p>`标签中。  

语法： `<p>段落文本</p>`    

注意一段文字一个`<p>`标签，如在一篇新闻文章中有3段文字，就要把这3个段落分别放到3个`<p>`标签中。如下图所示。  
![](http://upload-images.jianshu.io/upload_images/1408656-208f76dc1309d880.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
## **了解`<hx(1-6)>`标签，为你的网页添加标题**
文章的段落用`<p>`标签，那么文章的标题用什么标签呢？在本节我们将使用`<hx>`标签来制作文章的标题。  
标题标签一共有6个，h1、h2、h3、h4、h5、h6分别为一级标题、二级标题、三级标题、四级标题、五级标题、六级标题。并且依据重要性递减。`<h1>`是最高的等级。  

语法：`<hx>标题文本</hx> x:1-6`

注意：因为h1标签在网页中比较重要，所以一般h1标签被用在网站名称上。腾讯网站就是这样做的。如：`<h1>腾讯网</h1>`  

h1-h6标签的默认样式：  
标签代码：  
![](http://upload-images.jianshu.io/upload_images/1408656-7e2fdcbfcac38da1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
在浏览器中显示的样式：  
![](http://upload-images.jianshu.io/upload_images/1408656-53c0e5da7b284e32.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

---
## **加入强调语气，使用`<strong>`和`<em>`标签**
有了段落又有了标题，现在如果想在一段话中特别强调某几个文字，这时候就可以用到`<em>`或`<strong>`标签   
但两者在强调的语气上有区别:  
* `<em>` 表示强调，在浏览器中`<em>` 默认用斜体表示
* `<strong> `表示更强烈的强调，在浏览器中`<strong> `用粗体表示。
* 两个标签相比，目前国内前端程序员更喜欢使用`<strong>`表示强调。

在浏览器中默认样式是有区别的：
![](http://upload-images.jianshu.io/upload_images/1408656-dd990e2764178ca9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
浏览器中的样子，如下图。  
![](http://upload-images.jianshu.io/upload_images/1408656-c51d34355d1e9df5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


语法：     
`<em>需要强调的文本</em>  `  
`<strong>需要强调的文本</strong>`

栗子：  
在网上商城中，某产品的打折后的价格是需要强调的。如下图。   
![](http://upload-images.jianshu.io/upload_images/1408656-ce861d99a21e0719.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
代码实现:   
![](http://upload-images.jianshu.io/upload_images/1408656-735181aa80e24e5c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)   
 
---
## **加入上标下标，使用`<sup>`和`<sub>`标签**  
如果想在一段文字中加入上标或下标，就需要用到`<sup>`和`<sub>`标签。  
* `<sup>`表示上标。  
* `<sub>`表示下标。    


语法：  
`<sup>受影响的文字</sup>`  
`<sub>受影响的文字</sub>`  
栗子：  
```
<p>x<sub>1</sub>+y<sup>2</sup>=0</p>
```  
在浏览器中的显示效果：  
![](http://i.imgur.com/VAQww9q.jpg)

---
## **使用`<span>`标签为文字设置单独样式**
语法：`<span>文本</span>`

我们对`<em>`、`<strong>`、`<span>`这三个标签进行一下总结：

1. `<em>`和`<strong>`标签是为了强调一段话中的关键字时使用，它们的语义是强调。

2. `<span>`标签是没有语义的，它的作用就是为了设置单独的样式用的。

如果现在我们想把上一小节的第一段话“美国梦”三个字设置成blue（蓝色），但注意不是为了强调“美国梦”，而只是想为它设置和其它文字不同的样式（并不想让屏幕阅读器对“美国梦”这三个字加重音读出），所以这样情况下就可以用到`<span>`标签了。  
如下面例子：
```
<p>1922年的春天，一个想要成名名叫<em>尼克•卡拉威</em>（托比•马奎尔Tobey Maguire 饰）的作家，
离开了美国中西部，来到了纽约。那是一个道德感渐失，爵士乐流行，走私为王，<strong>股票</strong>飞涨的时代。
为了追寻他的<span>美国梦</span>，他搬入纽约附近一海湾居住。</p>
```
我们如果想设置“美国梦”三个字设置成blue（蓝色），只需要在`<style>`标签中加入：
```
span{
    color:blue;
}
```
css部分，以后会聊，你能大概明白span就是能干单独设置样式的活，就ok了  

---
## **`<q>`标签，短文本引用**
想在你的html中加一段引用吗？比如在你的网页的文章里想引用某个作家的一句诗，这样会使你的文章更加出彩，那么`<q>`标签是你所需要的。

语法：`<q>引用文本</q>`

栗子：  
```
<p>最初知道庄子，是从一首诗<q>庄生晓梦迷蝴蝶。望帝春心托杜鹃。
</q>开始的。虽然当时不知道是什么意思，只是觉得诗句挺特别。
后来才明白这个典故出自是庄子的《逍遥游》，《逍遥游》代表了庄子思想的最高境界，是对世俗社会的功名利禄及自己的舍弃。
</p>
```
讲解:  
1. 在上面的例子中，“庄生晓梦迷蝴蝶。望帝春心托杜鹃。” 这是一句诗歌，出自晚唐诗人李商隐的《锦瑟》 。因为不是作者自己的文字，所以需要使用<q></q>实现引用。

2. 注意要引用的文本不用加双引号，浏览器会对q标签自动添加双引号。

下图是代码显示结果：
![](http://upload-images.jianshu.io/upload_images/1408656-4692a324c924aae9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

注意这里用<q>标签的真正关键点不是它的默认样式双引号（如果这样我们不如自己在键盘上输入双引号就行了），而是它的语义：引用别人的话。

---
## **`<blockquote>`标签，长文本引用**
`<blockquote>`的作用也是引用别人的文本。但它是对长文本的引用，如在文章中引入大段某知名作家的文字，这时需要这个标签。
等等，上一节`<q>`标签不是也是对文本的引用吗？不要忘记`<q>`标签是对简短文本的引用，比如说引用一句话就用到`<q>`标签。  
如想在我的文章中引用李白《关山月》中的诗句，因为引用文本比较长，所以使用`<blockquote>`。  

语法：`<blockquote>引用文本</blockquote>`
如下面例子：
```
<blockquote>明月出天山，苍茫云海间。长风几万里，吹度玉门关。汉下白登道，胡窥青海湾。由来征战地，不见有人还。 戍客望边色，思归多苦颜。高楼当此夜，叹息未应闲。</blockquote>
```

浏览器对`<blockquote>`标签的解析是缩进样式。如下图所示：  
![](http://upload-images.jianshu.io/upload_images/1408656-95a03ac03144942d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

---
## **使用`<br>`标签分行显示文本**
例子，我们想让一首诗显示得更美观些，如显示下面效果：  
![](http://upload-images.jianshu.io/upload_images/1408656-92b64c3e19eed555.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
怎么可以让每一句诗词后面加入一个折行呢？那就可以用到`<br />`标签了，在需要加回车换行的地方加入`<br />`，`<br />`标签作用相当于word文档中的回车。  
代码改为：  
```
<h2>《咏桂》</h2>
<p>暗淡轻黄体性柔，<br />情疏迹远只香留。<br />何须浅碧深红色，<br />自是花中第一流。
```
诗文在浏览器中显示为：  
![](http://upload-images.jianshu.io/upload_images/1408656-0c48fe98c4eeba81.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
## **为你的网页中添加一些空格**
在html代码中输入空格、回车都是没有作用的。要想输入空格，必须写入`nbsp;`。**不要忘了那个分号**  

在html代码中输入空格是不起作用的，如下代码。  
![](http://upload-images.jianshu.io/upload_images/1408656-1ebb47c9ecdf60f6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在浏览中显示，还是没有空格效果。  
![](http://upload-images.jianshu.io/upload_images/1408656-a5b5ee97c3003e8a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

输入空格的正确方法：  
![](http://upload-images.jianshu.io/upload_images/1408656-42a825285c76c9d8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在浏览器中的显示出来的空格效果。如下图所示。  
![](http://upload-images.jianshu.io/upload_images/1408656-79b73ea87036171e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
## **认识`<hr>`标签，添加水平横线**
在信息展示时，有时会需要加一些用于分隔的横线，这样会使文章看起来整齐些。如下图所示：
![](http://upload-images.jianshu.io/upload_images/1408656-1efd16320da7923b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

语法：
* html4.01版本 `<hr>`
* xhtml1.0版本 `<hr />`  
注意：
1. `<hr />`标签和`<br />`标签一样也是一个空标签，所以只有一个开始标签，没有结束标签。
2. `<hr />`标签的在浏览器中的默认样式线条比较粗，颜色为灰色，可能有些人觉得这种样式不美观，没有关系，这些外在样式在我们以后学习了css样式表之后，都可以对其修改。
3. 大家注意，现在一般使用 xhtml1.0 的版本（其它标签也是），这种版本比较规范。

---
## **`<address>`标签，为网页加入地址信息**
一般网页中会有一些网站的联系地址信息需要在网页中展示出来，这些联系地址信息如公司的地址就可以`<address>`标签。也可以定义一个地址（比如电子邮件地址）、签名或者文档的作者身份。
栗子：  
```
<address>
本文的作者：<a href="mailto:zhaoliangsyn@163.com">zhaolion</a>
</address>
```
---
## **想加入一行代码吗？使用`<code>`标签**
在介绍语言技术的网站中，避免不了在网页中显示一些计算机专业的编程代码，当代码为一行代码时，你就可以使用`<code>`标签了，如下面例子：  

`<code>var i = a + b;</code>`  

注意：在文章中一般如果要插入多行代码时不能使用`<code>`标签了。**如果是多行代码，可以使用`<pre>`标签**。

---
## **使用`<pre>`标签为你的网页加入大段代码**
在上节中介绍加入一行代码的标签为`<code>`，但是在大多数情况下是需要加入大段代码的，如下图：
![](http://upload-images.jianshu.io/upload_images/1408656-e106fb471623dd29.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

怎么办？不会是每一代码都加入一个`<code>`标签吧，没有这么复杂，这时候就可以使用`<pre>`标签。  

语法：`<pre>语言代码段</pre>`

`<pre> `标签的主要作用:预格式化的文本。被包围在 pre 元素中的文本通常会保留空格和换行符。
如下代码：
```
<pre>
    var message="欢迎";
    for(var i=1;i<=10;i++)
    {
        alert(message);
    }
</pre>
```
在浏览器中的显示结果为：  
![](http://upload-images.jianshu.io/upload_images/1408656-cc2a4d8f5dd58d14.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

在上面的例子中可以看到代码中的空格，换行符都保留下来。如果用以前的方法，回车需要输入`<br>`签，空格需要输入` `  

注意：`<pre>` 标签不只是为显示计算机的源代码时用的，在你需要在网页中预显示格式时都可以使用它，只是`<pre>`标签的一个常见应用就是用来展示计算机的源代码。

---
## **使用`<ul>`，添加新闻信息列表**
在浏览网页时，你会发现网页上有很多信息的列表，如新闻列表、图片列表，如下图所示。  
![](http://upload-images.jianshu.io/upload_images/1408656-4fcab0089c52e3f4.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

这些列表就可以使用ul-li标签来完成。ul-li是 **没有前后顺序的信息列表**。

语法：  
```
<ul>
  <li>信息</li>
  <li>信息</li>
   ......
</ul>
```
举例：  
```
<ul>
  <li>精彩少年</li>
  <li>美丽突然出现</li>
  <li>触动心灵的旋律</li>
</ul>
```
ul-li在网页中显示的默认样式一般为：每项li前都自带一个圆点，如下图所示：  
![](http://upload-images.jianshu.io/upload_images/1408656-201fd31723b832b0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

---
## **使用`<ol>`，添加顺序列表**
如果想在网页中展示有前后顺序的信息列表，怎么办呢？如，当当网上的书籍热卖排行榜，如下图所示。这类信息展示就可以使用`<ol>`标签来制作有序列表来展示。  
![](http://upload-images.jianshu.io/upload_images/1408656-dc5b0325f8c02a0a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
语法：
```
<ol>
   <li>信息</li>
   <li>信息</li>
   ......
</ol>
```

举例：

下面是一个热点课程下载排行榜：  
```
<ol>
   <li>前端开发面试心法 </li>
   <li>零基础学习html</li>
   <li>JavaScript全攻略</li>
</ol>
```

`<ol>`在网页中显示的默认样式一般为：每项`<li>`前都自带一个序号，序号默认从1开始，如下图所示：  
![](http://upload-images.jianshu.io/upload_images/1408656-e1ca3e8946c64a49.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
## **初识`div`**

### **认识div在排版中的作用**
在网页制作过程过中，可以把一些独立的逻辑部分划分出来，放在一个<div>标签中，这个<div>标签的作用就相当于一个容器。  

语法：`<div>…</div>`

确定逻辑部分：  
什么是逻辑部分？它是页面上相互关联的一组元素。如网页中的独立的栏目版块，就是一个典型的逻辑部分。如下图所示：图中用红色边框标出的部分就是一个逻辑部分，就可以使用<div>标签作为容器。  
![](http://upload-images.jianshu.io/upload_images/1408656-6adffdc2132de7c6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

### **给div命名，使逻辑更加清晰**
在上一小节中，我们把一些标签放进`<div>`里，划分出一个独立的逻辑部分。为了使逻辑更加清晰，我们可以为这一个独立的逻辑部分设置一个名称，用id属性来为`<div>`提供唯一的名称，这个就像我们每个人都有一个身份证号，这个身份证号是唯一标识我们的身份的，也是必须唯一的。  
如下两图进行比较，如果设计师把两个图给你，哪个图你看上去能更快的理解呢？是不是右边的那幅图呢。  
![](http://upload-images.jianshu.io/upload_images/1408656-40b77682c34acb45.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

语法：`<div  id="版块名称">…</div>`

---
## **table标签，认识网页上的表格**

### **table标签 ＝ 我们平时看到到表格**
有时候我们需要在网页上展示一些数据，如某公司想在网页上展示公司的库存清单。如下表：  
![](http://upload-images.jianshu.io/upload_images/1408656-7174233c7ad09175.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
想在网页上展示上述表格效果可以使用以下代码：  
![](http://upload-images.jianshu.io/upload_images/1408656-5fd97e71afea23d1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

创建表格的四个元素： `table、tbody、tr、th、td`
1. `<table>…</table>`：整个表格以`<table>`标记开始、`</table>`标记结束。

2. `<tbody>…</tbody>`：当表格内容非常多时，表格会下载一点显示一点，但如果加上`<tbody>`标签后，这个表格就要等表格内容全部下载完才会显示。

3. `<tr>…</tr>`：表格的一行，所以有几对tr 表格就有几行。

4. `<td>…</td>`：表格的一个单元格，一行中包含几对`<td>...</td>`，说明一行中就有几列。

5. `<th>…</th>`：表格的头部的一个单元格，表格表头。

6. 表格中列的个数，取决于一行中数据单元格的个数。  

上述代码在浏览器中显示的默认的样式为：  
![](http://upload-images.jianshu.io/upload_images/1408656-edb64ee28e355e86.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

总结：

1. table表格在没有添加css样式之前，在浏览器中显示是没有表格线的

2. 表头，也就是th标签中的文本默认为粗体并且居中显示

### **用css样式，为表格加入边框**
Table 表格在没有添加 css 样式之前，是没有边框的。这样不便于我们后期合并单元格知识点的讲解，所以在这一节中我们为表格添加一些样式，为它添加边框。
代码中加入：  
```
<style type="text/css">
table tr td,th{border:1px solid #000;}
</style>
```
上述代码是用 css 样式代码，为th，td单元格添加粗细为一个像素的黑色边框。

结果窗口显示出结果样式：  
![](http://upload-images.jianshu.io/upload_images/1408656-aa796720ee26f16c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

### **caption标签，为表格添加标题和摘要**
表格还是需要添加一些标签进行优化，可以添加标题和摘要。代码如下  



![](http://upload-images.jianshu.io/upload_images/1408656-44be2f6d160ca9da.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
**摘要** 摘要的内容是不会在浏览器中显示出来的。它的作用是增加表格的可读性(语义化)，使搜索引擎更好的读懂表格内容，还可以使屏幕阅读器更好的帮助特殊用户读取表格内容。  
语法：`<table summary="表格简介文本">`  

**标题** 用以描述表格内容，标题的显示位置：表格上方。
语法：
```
<table>
    <caption>标题文本</caption>
    <tr>
        <td>…</td>
        <td>…</td>
        …
    </tr>
…
</table>
```

---
## **初识`<a>`标签**

### **使用`<a>`标签，链接到另一个页面**
使用`<a>`标签可实现超链接，它在网页制作中可以说是无处不在，只要有链接的地方，就会有这个标签。  

语法 ：  
`<a  href="目标网址"  title="鼠标滑过显示的文本">链接显示的文本</a>`  

例如：
`<a  href="http://www.zhaolion.com"  title="点击进入我的博客">click here!</a>`

上面例子作用是单击click here!文字，网页链接到`http://www.zhaolion.com`这个网页。  

title属性的作用，鼠标滑过链接文字时会显示这个属性的文本内容。这个属性在实际网页开发中作用很大，主要方便搜索引擎了解链接地址的内容（语义化更友好)
**提醒**   
还有一个有趣的现象不知道小伙伴们发现了没有，只要为文本加入a标签后，文字的颜色就会自动变为蓝色（被点击过的文本颜色为紫色），颜色很难看吧，不过没有关系后面我们学习了css样子就可以设置过来（a{color:#000}),后面会详细讲解。

### **在新建浏览器窗口中打开链接**
`<a>`标签在默认情况下，链接的网页是在当前浏览器窗口中打开，有时我们需要在新的浏览器窗口中打开。只需要添加一个属性 `target="_blank"`
如下代码：  
`<a href="目标网址" target="_blank">click here!</a>`  

###**图像链接**  
点击图片，跳到指定链接。  
如下代码：  
`<a  href="链接地址"> <img src="图像地址"> </a>`    

### **使用mailto在网页中链接Email地址**
`<a>`标签还有一个作用是可以链接Email地址，使用mailto能让访问者便捷向网站管理者发送电子邮件。我们还可以利用mailto做许多其它事情。下面一一进行讲解，请看详细图示：  
![](http://upload-images.jianshu.io/upload_images/1408656-685c72c34b17aeaf.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

**提醒**:如果mailto后面同时有多个参数的话，第一个参数必须以“?”开头，后面的参数每一个都以“&”分隔。  
下面是一个完整的实例:  在浏览器中显示的一个发送按钮
![](http://upload-images.jianshu.io/upload_images/1408656-d4df48e06e4d1e8e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)   

点击链接会打开电子邮件应用，并自动填写收件人等设置好的信息，如下图：
![](http://upload-images.jianshu.io/upload_images/1408656-f72e87f66a489541.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

---
## **认识`<img>`标签，为网页插入图片**
在网页的制作中为使网页炫丽美观，肯定是缺少不了图片，可以使用`<img>`标签来插入图片。  
语法： `[站外图片上传中……(48)]`  

举例： `<img src = "myimage.gif" alt = "My Image" title = "My Image" />`  

讲解：

1. src：标识图像的位置；

2. alt：指定图像的描述性文本，当图像不可见时（下载不成功时），可看到该属性指定的文本；

3. title：提供在图像可见时对图像的描述(鼠标滑过图片时显示的文本)；

4. 图像可以是GIF，PNG，JPEG格式的图像文件。  

---
## **认识表单**

### **使用表单标签，与用户交互**
网站怎样与用户进行交互？答案是使用HTML表单(form)。表单是可以把浏览者输入的数据传送到服务器端，这样服务器端程序就可以处理表单传过来的数据。  

语法： `<form   method="传送方式"   action="服务器文件">`  

讲解：
1. `<form>` ：`<form>`标签是成对出现的，以`<form>`开始，以`</form>`结束。

2. action ：浏览者输入的数据被传送到的地方,比如一个PHP页面(save.php)。

3. method ： 数据传送的方式（get/post）。
```
<form    method="post"   action="save.php">
        <label for="username">用户名:</label>
        <input type="text" name="username" />
        <label for="pass">密码:</label>
        <input type="password" name="pass" />
</form>
```

**注意**  
1. 所有表单控件（文本框、文本域、按钮、单选框、复选框等）都必须放在`<form></form>`标签之间（否则用户输入的信息可提交不到服务器上哦！）。

2. method:post/get的区别这一部分内容属于后端程序员考虑的问题。感兴趣的小伙伴可以问谷哥  

### **文本输入框、密码输入框**
当用户要在表单中键入字母、数字等内容时，就会用到文本输入框。文本框也可以转化为密码输入框。

语法：
```
<form>
   <input type="text/password" name="名称" value="文本" />
</form>
```

1. type：

   * 当type="text"时，输入框为文本输入框;
   * 当type="password"时, 输入框为密码输入框。

2. name：为文本框命名，以备后台程序ASP 、PHP使用。

3. value：为文本输入框设置默认值。(一般起到提示作用)

举例：

```
<form>
  姓名：
  <input type="text" name="myName">
  <br/>
  密码：
  <input type="password" name="pass">
</form>
```
在浏览器中显示的结果：
![](http://upload-images.jianshu.io/upload_images/1408656-cc5f4bc6933358ef.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

### **文本域，支持多行文本输入**
当用户需要在表单中输入大段文字时，需要用到文本输入域。  

语法： `<textarea  rows="行数" cols="列数">文本</textarea>`  

1. `<textarea>`标签是成对出现的，以`<textarea>`开始，以`</textarea>`结束。

2. cols ：多行输入域的列数。

3. rows ：多行输入域的行数。

4. 在`<textarea></textarea>`标签之间可以输入默认值。

举例：  
```
<form  method="post" action="save.php">
        <label>联系我们</label>
        <textarea cols="50" rows="10" >在这里输入内容...</textarea>
</form>
```
在浏览器中显示结果：
![](http://upload-images.jianshu.io/upload_images/1408656-8ea27ed167f633c2.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### **使用单选框、复选框，让用户选择**
在使用表单设计调查表时，为了减少用户的操作，使用选择框是一个好主意，html中有两种选择框，即单选框和复选框，两者的区别是单选框中的选项用户只能选择一项，而复选框中用户可以任意选择多项，甚至全选。请看下面的例子:  
语法： `<input   type="radio/checkbox"   value="值"    name="名称"   checked="checked"/>`

1. type:

   * 当 type="radio" 时，控件为单选框

   * 当 type="checkbox" 时，控件为复选框

2. value：提交数据到服务器的值（后台程序PHP使用）

3. name：为控件命名，以备后台程序 ASP、PHP 使用

4. checked：当设置 checked="checked" 时，该选项被默认选中

如下面代码：    
![](http://upload-images.jianshu.io/upload_images/1408656-aad335d9143cf821.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)   

在浏览器中显示的结果：  
![](http://upload-images.jianshu.io/upload_images/1408656-c23dc7d1b061e68f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)   

**注意**:同一组的单选按钮，name 取值一定要一致，比如上面例子为同一个名称“radioLove”，这样同一组的单选按钮才可以起到单选的作用。

### **使用下拉列表框，节省空间**
下拉列表在网页中也常会用到，它可以有效的节省网页空间。既可以单选、又可以多选。如下代码：  
![](http://upload-images.jianshu.io/upload_images/1408656-0cf73d620413983a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
讲解：

1. value：
![](http://upload-images.jianshu.io/upload_images/1408656-f16609edfb448272.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
2. selected="selected"：设置selected="selected"属性，则该选项就被默认选中。

### **使用提交按钮，提交数据**
在表单中有两种按钮可以使用，分别为：提交按钮、重置。这一小节讲解提交按钮：当用户需要提交表单信息到服务器时，需要用到提交按钮。  
语法： `<input   type="submit"   value="提交">`  
1. type：只有当type值设置为submit时，按钮才有提交作用
2. value：按钮上显示的文字  

举例：  
![](http://upload-images.jianshu.io/upload_images/1408656-772c2b6947f1d735.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

在浏览器中显示的结果：  
![](http://upload-images.jianshu.io/upload_images/1408656-adeb74f1d08c1507.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### **使用重置按钮，重置表单信息**
当用户需要重置表单信息到初始时的状态时，比如用户输入“用户名”后，发现书写有误，可以使用重置按钮使输入框恢复到初始状态。只需要把type设置为"reset"就可以。  
语法： `<input type="reset" value="重置">`  
1. type：只有当type值设置为reset时，按钮才有重置作用  
2. value：按钮上显示的文字  

举例：  

![](http://upload-images.jianshu.io/upload_images/1408656-9702a67644028f6e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

在浏览器中显示的结果：  
输入账号    
![](http://upload-images.jianshu.io/upload_images/1408656-f6126a98d4370c4d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)   
单击重置按钮   
![](http://upload-images.jianshu.io/upload_images/1408656-453fb9f9e7fe4e7a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

***input标记中type类型***    
  
|值|描述|
|---|---|
|button|定义可点击按钮（多数情况下，用于通过JavaScript启动脚本）|
|checkbox|定义复选框|
|file|定义输入字段和"浏览"按钮，供文件上传|
|hidden|定义隐藏的输入字段|
|image|定义图像形式的提交按钮|
|password|定义密码字段。该字段中的字符被掩码。|
|radio|定义单选按钮。|
|reset|定义重置按钮。重置按钮会清除表单中的所有数据。|
|submit|定义提交按钮。提交按钮会把表单数据发送到服务器。 |
|text|定义单行的输入字段，用户可在其中输入文本。默认宽度为20个字符。|   
|email|用于应该包含 e-mail 地址的输入域|  
|URL|用于应该包含 e-mail 地址的输入域|
|number|用于应该包含数值的输入域,还能够设定对所接受的数字的限定|
|range|包含一定范围内数字值的输入域,外观为一个滑动条|
|date|选取日、月、年|
|color|颜色选择器用于挑选色彩，外观为一个取色器|

### **使用下拉列表框进行多选**
下拉列表也可以进行多选操作，在`<select>`标签中设置`multiple="multiple"`属性，就可以实现多选功能，在 widows 操作系统下，进行多选时按下Ctrl键同时进行单击（在 Mac下使用 Command +单击），可以选择多个选项。如下代码：  
![](http://upload-images.jianshu.io/upload_images/1408656-cd50b0431454da5e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)   

在浏览器中显示的结果：  
![](http://upload-images.jianshu.io/upload_images/1408656-60cd462bb13e1634.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  


### **form表单中的label标签**
小伙伴们，你们在前面学习表单各种控件的时候，有没有发现一个标签--label，这一小节就来揭晓它的作用。  
label标签不会向用户呈现任何特殊效果，它的作用是为鼠标用户改进了可用性。如果你在 label 标签内点击文本，就会触发此控件。就是说，当用户单击选中该label标签时，浏览器就会自动将焦点转到和标签相关的表单控件上（就自动选中和该label标签相关连的表单控件上）。  
语法： `<label for="控件id名称">`  
**注意** 标签的 for 属性中的值应当与相关控件的 id 属性值一定要相同。 **这样你会在点慢跑标签，即使没有点checkbox 也能选中**  
例子：
```
<form>
  <a>你对什么运动感兴趣：</a> <br />
  <label for="1">慢跑</label><input type="checkbox" name="manpao" id="1"><br />
  <label for="2">登山</label><input type="checkbox" name="dengshan" id="2"><br />
  <label for="3">篮球</label><input type="checkbox" name="lanqiu" id="3"><br />
</form>
```
