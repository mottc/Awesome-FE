## 引言
这次给大家带来了CSS－盒子模型部分的笔记，大家一同交流😊

认识盒子模型之前，先来了解一下CSS元素的分类吧，后面再细细道来～

## CSS元素分类
在CSS中，html中的标签元素大体被分为三种不同的类型：
* 块状元素
* 内联元素(又叫行内元素)
* 内联块状元素

常用的块状元素有：
`<div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>、<table>、<address>、<blockquote> 、<form>`

常用的内联元素有：
`<a>、<span>、<br>、<i>、<em>、<strong>、<label>、<q>、<var>、<cite>、<code>`

常用的内联块状元素有:  
`<img>、<input>`

### **元素分类--块级元素**
什么是块级元素？在html中`<div>、 <p>、<h1>、<form>、<ul> 、 <li>`就是块级元素。设置`display:block`就是将元素显示为块级元素。
如下代码就是将内联元素a转换为块状元素，从而使a元素具有块状元素特点。  
`a{display:block;}`

块级元素特点：
* 每个块级元素都从新的一行开始，并且其后的元素也另起一行。（真霸道，一个块级元素独占一行）
* 元素的高度、宽度、行高以及顶和底边距都可设置。
* 元素宽度在不设置的情况下，是它本身父容器的100%（和父元素的宽度一致），除非设定一个宽度。

### **元素分类--内联元素**
在html中，`<span>、<a>、<label>、 <strong> 、<em>`就是典型的内联元素（行内元素）（inline）元素。  
当然块状元素也可以通过代码`display:inline`将元素设置为内联元素。如下代码就是将块状元素div转换为内联元素，从而使 div 元素具有内联元素特点。
```
div{
    display:inline;
}

......

<div>我要变成内联元素</div>
```
内联元素特点：
* 和其他元素都在一行
* 元素的高度、宽度及顶部和底部边距不可设置
* 元素的宽度就是它包含的文字或图片的宽度，不可改变。

**友情提示**：行内元素之间会产生间隙bug问题的场景：  
当行内元素之间有“回车”、“tab”、“空格”时就会出现间隙。
如下代码：
```
<div>
   <a>1</a>
   <a>2</a>
   <span>33333</span>
   <span>44444</span>
   <em>555555</em>
</div>
```
解决方法：
1. 写在一行，之间不要有空格之类的符号。
2. 使用font-size:0   
```
div{font-size:0;}
a,span,em{font-size:16px;}
```

### **元素分类--内联块状元素**
内联块状元素（inline-block）就是同时具备内联元素、块状元素的特点，代码`display:inline-block`就是将元素设置为内联块状元素。(css2.1新增)  
`<img>、<input>`标签就是这种内联块状标签。

inline-block 元素特点：  
1. 和其他元素都在一行上；

2. 元素的高度、宽度、行高以及顶和底边距都可设置。

**友情提示** 平时开发时候 a 元素设置了宽和高，但都没有起到作用，原因是a在默认的时候是内联元素，内联元素是不可以设置宽和高的  


## css盒子模型
在网页设计中常听的属性名：内容(content)、填充/内边距(padding)、边框(border)、外边距(margin)， CSS盒子模式都具备这些属性。
这些属性我们可以把它转移到我们日常生活中的盒子（箱子）上来理解，日常生活中所见的盒子也就是能装东西的一种箱子，也具有这些属性，所以叫它盒子模型。  

可以把它当成日常中的一个盒子去理解。content就是盒子里装的东西，它有高度（height）和宽度（width）,可以是图片，可以是文字或者小盒子嵌套，在现实中，内容不能大于盒子，内容大于盒子就会撑破盒子，但在css中，盒子有弹性的，顶多内容太大就会撑大盒子，但是不会损害盒子。
padding即是填充，就好像我们为了保证盒子里的东西不损坏，填充了一些东西，比如泡沫或者塑料薄膜，填充物有大有小，有软有硬，反应在网页中就是padding的大小了。而再外一层就是border边框，因为边框有大小和颜色的属性，相当于盒子的厚度和它的颜色或者材料。margin外边距，就是我们的盒子与其他的盒子或者其他东西的距离。假如有很多盒子，margin就是盒子堆码直接的距离，可以通风，也美观同时方便取出。  
我们理解了盒子模型，有助于我们了解一个元素的最终尺寸是怎么样决定的，同时也帮助我们理解元素在网页上是如何定位的。

![](http://upload-images.jianshu.io/upload_images/1408656-688353a5969cab8e.gif?imageMogr2/auto-orient/strip)  

盒子模型的三维立体结构图  

![](http://upload-images.jianshu.io/upload_images/1408656-b91bdd5bf15785e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

边框（border），位于盒子的第一层。
* 元素内容（content）、内边距（padding），两者同位于第二层。
* 背景图（background-image），位于第三层。
* 背景色（background-color），位于第四层。
* 整个盒子的外边距（margin），位于第五层。


### 盒模型的大小--宽度和高度

![](http://upload-images.jianshu.io/upload_images/1408656-c69130e8cb584d2b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

盒模型宽度和高度和我们平常所说的物体的宽度和高度理解是不一样的，css内定义的宽（width）和高（height），指的是填充以里的内容范围。  

因此一个 **元素实际宽度（盒子的宽度）=左边界+左边框+左填充+内容宽度+右填充+右边框+右边界**。    

元素的高度也是同理。    

![](http://upload-images.jianshu.io/upload_images/1408656-c9b42463ee960909.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

比如：
css代码：
```
div{
    width:200px;
    padding:20px;
    border:1px solid red;
    margin:10px;    
}
```
html代码：  
```
<body>
   <div>文本内容</div>
</body>
```
元素的实际长度为：10px+1px+20px+200px+20px+1px+10px=262px。在chrome浏览器下可查看元素盒模型，如下图：  
![](http://upload-images.jianshu.io/upload_images/1408656-98bf7fdce25a0ec5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  


### 插曲－标准 W3C 盒子模型 与 IE 盒模型对比
上面介绍的是我们熟悉的标准 W3C 盒子模型，然后古老的IE有一个自己的盒子模型，这里插一点新知识

**标准 W3C 盒子模型**     
标准 W3C 盒子模型的范围包括 margin、border、padding、content，并且 content 部分不包含其他部分。

![](http://upload-images.jianshu.io/upload_images/1408656-7fb37d4da3d93dfb.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**IE 盒子模型**     
 IE 盒子模型的范围也包括 margin、border、padding、content，和标准 W3C 盒子模型不同的是：IE 盒子模型的 content 部分包含了 border 和 pading。
![](http://upload-images.jianshu.io/upload_images/1408656-af2b13c17ef01dc0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

那应该选择哪中盒子模型呢？当然是“标准 W3C 盒子模型”了。怎么样才算是选择了“标准 W3C 盒子模型”呢？很简单，就是在网页的顶部加上 DOCTYPE 声明。如果不加 DOCTYPE 声明，那么各个浏览器会根据自己的行为去理解网页，即 IE 浏览器会采用 IE 盒子模型去解释你的盒子，而 FF 会采用标准 W3C 盒子模型解释你的盒子，所以网页在不同的浏览器中就显示的不一样了。反之，如果加上了 DOCTYPE 声明，那么所有浏览器都会采用标准 W3C 盒子模型去解释你的盒子，网页就能在各个浏览器中显示一致了。


### 盒模型--边框 - border
元素的边框 (border) 是围绕元素内容和内边距的一条或多条线。  

CSS border 属性允许你规定元素边框的样式、宽度和颜色。
盒子模型的边框就是围绕着内容及补白的线，这条线你可以设置它的粗细、样式和颜色(边框三个属性)。  

```
border: [<br-width> || <br-style> || <color>] | inherit
border-width: [<length> | thin | medium | thick]{1,4} | inherit
border-style: [solid | dashed | dotted | ...]{1,4} |inherit
border-colro: [<color> | transparent]{1,4} | inherit
```

如下面代码为 div 来设置边框粗细为 2px、样式为实心的、颜色为红色的边框：  
```
div{
    border:2px  solid  red;
}
```
上面是 border 代码的缩写形式，可以分开写：  
```
div{
    border-width:2px;
    border-style:solid;
    border-color:red;
}
```
**注意：**  
1. border-style（边框样式）常见样式有：`dashed（虚线）| dotted（点线）| solid（实线）`.
2. border-color（边框颜色）中的颜色可设置为十六进制颜色，如:`border-color:#888;//前面的井号不要忘掉`.
3. border-width（边框宽度）中的宽度也可以设置为：`thin | medium | thick（但不是很常用），最常还是用象素（px）`.

现在有一个问题，如果有想为 p 标签单独设置下边框，而其它三边都不设置边框样式怎么办呢？css 样式中允许只为一个方向的边框设置样式：  
`div{border-bottom:1px solid red;}`

同样可以使用下面代码实现其它三边(上、右、左)边框的设置:
```
border-top:1px solid red;
border-right:1px solid red;
border-left:1px solid red;
```

![](http://upload-images.jianshu.io/upload_images/1408656-d686b66e36b4ef41.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**border-radius**   

方方正正的边框很多时候让人感觉设计不够优雅，圆角矩形的边框此时不妨来尝试一下

```
/* 水平半径/垂直半径 */
border-radius: [ <length> | <percentage> ]{1,4} [ / [ <length> | <percentage> ]{1,4} ]?
```

![](http://upload-images.jianshu.io/upload_images/1408656-bdb08b46262e82ed.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 盒模型--填充(内边距)- padding
CSS padding 属性定义元素边框与元素内容之间的空白区域.

元素内容与边框之间是可以设置距离的，称之为“填充”。填充也可分为上、右、下、左(顺时针)。如下代码：
`div{padding:20px 10px 15px 30px;}`
顺序一定不要搞混。可以分开写上面代码：  
```
div{
   padding-top:20px;
   padding-right:10px;
   padding-bottom:15px;
   padding-left:30px;
}
```
如果上、右、下、左的填充都为10px;可以这么写  `div{padding:10px;}`  
如果上下填充一样为10px，左右一样为20px，可以这么写：  `div{padding:10px 20px;}`  

### 盒模型--外边距- margin
设置外边距的最简单的方法就是使用 margin 属性。  
margin 属性接受任何长度单位，可以是像素、英寸、毫米或 em。  
margin 可以设置为 auto。更常见的做法是为外边距设置长度值。下面的声明在 h1 元素的各个边上设置了 1/4 英寸宽的空白：  
`h1 {margin : 0.25in;}`
下面的例子为 h1 元素的四个边分别定义了不同的外边距，所使用的长度单位是像素 (px)：  
`h1 {margin : 10px 0px 15px 5px;}`

与内边距的设置相同，这些值的顺序是从上外边距 (top) 开始围着元素顺时针旋转的：  `margin: top right bottom left`
另外，还可以为 margin 设置一个百分比数值：  `p {margin : 10%;}`,百分数是相对于父元素的 width 计算的。上面这个例子为 p 元素设置的外边距是其父元素的 width 的 10%。

### 盒模型属性 － overflow

overflow 属性规定当内容溢出元素框时发生的事情。

这个属性定义溢出元素内容区的内容会如何处理。如果值为 scroll，不论是否需要，用户代理都会提供一种滚动机制。因此，有可能即使元素框中可以放下所有内容也会出现滚动条。

| 值      | 描述                                                     |
|:--------|:---------------------------------------------------------|
| visible | 默认值。内容不会被修剪，会呈现在元素框之外。             |
| hidden  | 内容会被修剪，并且其余内容是不可见的。                   |
| scroll  | 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。 |
| auto    | 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。 |
| inherit | 规定应该从父元素继承 overflow 属性的值。                 |

![](http://upload-images.jianshu.io/upload_images/1408656-7c27cdba66178329.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 盒模型属性 －box-shadow
box-shadow 属性向框添加一个或多个阴影。
语法:     
`box-shadow: h-shadow v-shadow blur spread color inset;`

```

box-shadow: 4px  6px   3px  0px red;
             |    |     |    |
          水平偏移 |     |    |
               垂直偏移  |    |
                    模糊半径  |
                          阴影大小
```

注意：水平与垂直偏移可以为负值即相反方向偏移。颜色默认为文字颜色。阴影不占据空间，仅为修饰效果。

![](http://upload-images.jianshu.io/upload_images/1408656-adae161942204e34.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### TRBL
TRBL (Top, Right, Bottom, Left) 即为顺时针从顶部开始。具有四个方向的属性都可以通过 `*-top *-right *-bottom 与 *-left` 单独对其进行设置。

![](http://upload-images.jianshu.io/upload_images/1408656-7a68de9f09c01439.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 值缩写
下面的值缩写以 padding 为例。     
>对面相等，后者省略；四面相等，只设一个。

```
/*      四面值 */
padding: 20px;
padding: 20px 20px 20px 20px;

/*      上下值 右左值 */
padding: 20px   10px;
padding: 20px 10px 20px 10px;

/*       上值 右左值 下值 */
padding: 20px 10px   30px;
padding: 20px 10px 30px 10px;
```


### CSS 外边距合并
**外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。**   
**合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。**  

外边距合并   

外边距合并（叠加）是一个相当简单的概念。但是，在实践中对网页进行布局时，它会造成许多混淆。   
简单地说，外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。
当一个元素出现在另一个元素上面时，第一个元素的下外边距与第二个元素的上外边距会发生合并。请看下图：   

![](http://upload-images.jianshu.io/upload_images/1408656-80168c75b31eb8a9.gif?imageMogr2/auto-orient/strip)  

当一个元素包含在另一个元素中时（假设没有内边距或边框把外边距分隔开），它们的上和/或下外边距也会发生合并。请看下图：    

![](http://upload-images.jianshu.io/upload_images/1408656-7cfa2a2de02b6a02.gif?imageMogr2/auto-orient/strip)    

尽管看上去有些奇怪，但是外边距甚至可以与自身发生合并。

假设有一个空元素，它有外边距，但是没有边框或填充。在这种情况下，上外边距与下外边距就碰到了一起，它们会发生合并：    

![](http://upload-images.jianshu.io/upload_images/1408656-7fcf527463bfde64.gif?imageMogr2/auto-orient/strip)    

如果这个外边距遇到另一个元素的外边距，它还会发生合并：   

![](http://upload-images.jianshu.io/upload_images/1408656-5efe89e9023eb794.gif?imageMogr2/auto-orient/strip)    

这就是一系列的段落元素占用空间非常小的原因，因为它们的所有外边距都合并到一起，形成了一个小的外边距。

外边距合并初看上去可能有点奇怪，但是实际上，它是有意义的。以由几个段落组成的典型文本页面为例。第一个段落上面的空间等于段落的上外边距。如果没有外边距合并，后续所有段落之间的外边距都将是相邻上外边距和下外边距的和。这意味着段落之间的空间是页面顶部的两倍。如果发生外边距合并，段落之间的上外边距和下外边距就合并在一起，这样各处的距离就一致了。  

![](http://upload-images.jianshu.io/upload_images/1408656-aa9166ab6595a493.gif?imageMogr2/auto-orient/strip)  

注释：只有普通文档流中块框的垂直外边距才会发生外边距合并。行内框、浮动框或绝对定位之间的外边距不会合并。
