# 引言

本人在慕课网学习[HTML+CSS基础课程](http://www.imooc.com/learn/9)，记录一些文字，方便自己回忆，也希望对大家有所帮助

上次给大家带来了html部分的笔记，大家的反馈让我非常开心😄。

这次给大家带来css部分的第一篇笔记，由于本人比较蠢，学的很慢，而且css部分内容非常的细、广，需要不断code，才能体会其中细节，因此这次暂时只能带来本人已经整理好一部分，以供大家一同进步。

另外有一个求助，Atom中Toc插件生成页面，无法在Github或者简书中使用，希望有知道解决方法的高手，能够给予帮助

---
# CSS入门笔记 － 初识CSS


## 1 - 认识CSS样式

CSS全称为“层叠样式表 (Cascading Style Sheets)”，它主要是用于定义HTML内容在浏览器内的显示样式，如文字大小、颜色、字体加粗等用于设置页面的表现。CSS3 并不是一个完整的独立版本而是将不同的功能拆分成独立模块（例如，选择器模块，盒模型模块），这有利于不同功能的及时更新与发布也利于浏览器厂商的实际使用。

---
## 2 - 为何使用CSS？
CSS帮助您将文档信息的内容 和如何展现它的细节相分离。众所周知，如何展现文档的细节即为样式(style)。您可以将样式从它的内容分离出来，以便您能够：
* 避免重复
* 更容易维护
* 为不同的目的，使用不同的样式而内容相同

例如:  
您的网站可能有成千上万的页面外观相似。使用CSS，您可以将样式信息存储在公共的文件中以供所有的页面共用。

当用户显示页面时，用户的浏览器将样式信息和页面内容一同加载。

当用户打印页面时，您可以提供不同的样式信息，以便于打印出来的页面更易于阅读。

总之，在HTML中，您使用标记语言来描述文档的内容而不是它的样式。您可以使用CSS来指定它的样式而不是它的内容。

---
## 3 - CSS语法

CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明:  
![](http://upload-images.jianshu.io/upload_images/1408656-558529e1c6176917.gif?imageMogr2/auto-orient/strip)

**选择器**：指明网页中要应用样式规则的元素，如本例中是网页中所有的段（p）的文字将变成红色，而其他的元素（如ol）不会受到影响。

**声明**：在英文大括号“｛｝”中的的就是声明，属性和值之间用英文冒号“：”分隔。当有多条声明时，中间可以英文分号“;”分隔，如下所示：

```
p {
    color:red;
    text-align:center;
}
```

CSS 注释  
注释是用来解释你的代码，并且可以随意编辑它，浏览器会忽略它。
CSS注释以 `/*` 开始, 以 `*/` 结束, 实例如下:  
```
/* p标签的样式 */
p {
    text-align:center; /* 文本居中 */
    color:black;
    font-family:arial;
}
```

---
## 4 - CSS样式引入
CSS样式可以写在哪些地方呢？从CSS 样式代码插入的形式来看基本可以分为以下3种：
>* 内联式css样式
>* 嵌入式CSS样式
>* 外部式CSS样式

### 4.1 - 内联式css样式  
内联式css样式表就是把css代码直接写在现有的HTML标签中，如下面代码：  
`<p style="color:red">这里文字是红色。</p>`  
注意要写在元素的开始标签里，下面这种写法是错误的：  
`<p>这里文字是红色。</p style="color:red">`  
并且css样式代码要写在style=""双引号中，如果有多条css样式代码设置可以写在一起，中间用分号隔开。如下代码：  
`<p style="color:red;font-size:12px">这里文字是红色。</p>`
### 4.2 - 嵌入式css样式  
嵌入式css样式，就是可以把css样式代码写在`<style type="text/css"></style>`标签之间。如下面代码实现把三个`<span>`标签中的文字设置为红色：   
```
<style type="text/css">
span {
    color:red;
}
</style>
```
嵌入式css样式必须写在`<style></style>`之间，并且一般情况下嵌入式css样式写在`<head></head>`之间。
### 4.3 - 外部式css样式  
外部式css样式(也可称为外联式)就是把css代码写一个单独的外部文件中，这个css样式文件以“.css”为扩展名，在`<head>`内（不是在`<style>`标签内）使用`<link>`标签将css样式文件链接到HTML文件内，如下面代码：   
`<link href="base.css" rel="stylesheet" type="text/css" />`
>注意：  
> 1. css样式文件名称以有意义的英文字母命名，如 main.css.
> 2. rel="stylesheet" type="text/css" 是固定写法不可修改。
> 3. <link>标签位置一般写在<head>标签之内。

### 4.4 - 三种方法的优先级  
内联式 > 嵌入式 > 外部式  
但是嵌入式>外部式有一个前提：嵌入式css样式的位置一定在外部式的后面,`<link href="style.css" ...>`代码在`<style type="text/css">...</style>`代码的前面（实际开发中也是这么写的）

---
## 5 － css选择器
什么是选择器？  
每一条css样式声明（定义）由两部分组成，形式如下：  
```
选择器{
    样式;
}
```
在{}之前的部分就是“选择器”，“选择器”指明了{}中的“样式”的作用对象，也就是“样式”作用于网页中的哪些元素。比如右侧代码编辑器中第7行代码中的“body”就是选择器。

### 5.1 － 简单选择器
简单选择器可组合使用。
#### 5.1.1 － 标签选择器
标签选择器其实就是html代码中的标签。如右侧代码编辑器中的`<html>、<body>、<h1>、<p>、<img>`。例如下面代码：
```
p{font-size:12px;line-height:1.6em;}  
```
上面的css样式代码的作用：为p标签设置12px字号，行间距设置1.6em的样式。

#### 5.1.2 － 类选择器
类选择器在css样式编码中是最常用到的
.className 以 . 开头，名称可包含字母，数字，`-`，`_`，但必须以字母开头。它区分大小写并可出现多次。
语法：  
`.类选器名称{css样式代码;}`  

注意：
1. 英文圆点开头
2. 其中类选器名称可以任意起名（但不要起中文噢）

使用方法：  
第一步：使用合适的标签把要修饰的内容标记起来，如下：  
`<span>胆小如鼠</span>`  
第二步：使用class="类选择器名称"为标签设置一个类，如下：  
`<span class="stress">胆小如鼠</span> `  
第三步：设置类选器css样式，如下：  
```
/*类前面要加入一个英文圆点*/
.stress {
    color:red;
}
```

#### 5.1.3 － ID选择器
`#idName `以 # 开头且只可出现一次，其命名要求于 .className 相同。在很多方面，ID选择器都类似于类选择符，但也有一些重要的区别：
1. 为标签设置id="ID名称"，而不是class="类名称"。
2. ID选择符的前面是井号（#）号，而不是英文圆点（.）。
3. ID选择器只能在文档中使用一次。与类选择器不同，在一个HTML文档中，ID选择器只能使用一次，而且仅一次。而类选择器可以使用多次。
4. 可以使用类选择器词列表方法为一个元素同时设置多个样式。我们可以为一个元素同时设多个样式，但只可以用类选择器的方法实现，ID选择器是不可以的（不能使用 ID 词列表）。

栗子：  
```
<div>
  <p id="special">Sample Paragraph</p>
</div>

<style type="text/css">
  #special {
    color: red;
  }
</style>
```

#### 5.1.4 － 通配符选择器
通用选择器是功能最强大的选择器，它使用一个（`*`）号指定，它的作用是匹配html中所有标签元素，如下使用下面代码使用html中任意标签元素字体颜色全部设置为红色：  
`* {color:red;}`  

#### 5.1.5 － 属性选择器
对带有指定属性的 HTML 元素设置样式。  
可以为拥有指定属性的 HTML 元素设置样式，而不仅限于 class 和 id 属性。  
注释：只有在规定了 !DOCTYPE 时，IE7 和 IE8 才支持属性选择器。在 IE6 及更低的版本中，不支持属性选择。

* [attr] 或 [attr=val] 来选择相应的元素。#nav{...} 既等同于 [id=nav]{...}。_IE7+_
* [attr~=val] 可选用与选择包含 val 属性值的元素，像class="title sports" 与 class="sports"。.sports{...} 既等同于 [class~=sports]{...} _IE7+_
* [attr|=val] 可以选择val开头及开头紧接-的属性值。_IE7+_
* [attr^=val] 可选择以val开头的属性值对应的元素，如果值为符号或空格则需要使用引号 ""。_IE7+_
* [attr$=val] 可选择以val结尾的属性值对应的元素。_IE7+_
* [attr*=val] 可选择以包含val属性值对应的元素。_IE7+_

**下面的选择器，强烈建议写代码尝试，效果更加直观，或者查看w3school的[属性选择器](http://www.w3school.com.cn/css/css_syntax_attribute_selector.asp)部分进行学习**

1 属性选择器
下面的例子为带有 title 属性的所有元素设置样式：  
```
[title] {
    color:red;
}
```
2 属性和值选择器  
下面的例子为 title="MyBlog" 的所有元素设置样式：  
```
[title=MyBlog] {
    border:5px solid blue;
}
```

3 属性和值选择器 - 多个值  
下面的例子为包含指定值的 title 属性的所有元素设置样式。适用于由空格分隔的属性值：
```
[title~=hello] {
    color:red;
}
```
下面的例子为带有包含指定值的 lang 属性的所有元素设置样式。适用于由连字符分隔的属性值：
```
[lang|=en] { color:red; }
```
4 设置表单的样式
属性选择器在为不带有 class 或 id 的表单设置样式时特别有用：
```
input[type="text"]
{
  width:150px;
  display:block;
  margin-bottom:10px;
  background-color:yellow;
  font-family: Verdana, Arial;
}

input[type="button"]
{
  width:120px;
  margin-left:35px;
  display:block;
  font-family: Verdana, Arial;
}
```
#### 5.1.6 － 伪类选择符
更有趣的是伪类选择符，为什么叫做伪类选择符，它允许给html不存在的标签（标签的某种状态）设置样式，比如说我们给html中一个标签元素的鼠标滑过的状态来设置字体颜色：  
`a:hover{color:red;}`  
上面一行代码就是为 a 标签鼠标滑过的状态设置字体颜色变红。这样就会使第一段文字内容中的“胆小如鼠”文字加入 **鼠标滑过字体** 颜色变为红色特效。   
常用伪类选择器：
- :link     _IE6+_
- :visited      _IE7+_
- :hover      _IE6中仅可用于链接_
- :active      _IE6/7中仅可用于链接_
- :enabled      _IE9+_
- :disabled      _IE9+_
- :checked      _IE9+_
- :first-child      _IE8+_
- :last-child      _IE9+_
- :nth-child(even) 可为 odd even 或数字      _IE9+_
- :nth-last-child(n) n从 0 开始计算      _IE9+_
- :only-child 仅选择唯一的元素      _IE9+_
- :only-of-type      _IE9+_
- :first-of-type      _IE9+_
- :last-of-type      _IE9+_
- :nth-of-type(even)      _IE9+_
- :nth-last-of-type(2n)      _IE9+_

不常用伪类选择器：
- :empty 选中页面中无子元素的标签      _IE9+_
- :root 选择 HTML 根标签      _IE9+_
- :not() 参数为一般选择器      _IE9+_
- :target 被锚点选中的目标元素      _IE9+_
- :lang() 选中语言值为某类特殊值的元素      _IE7+_

注意：
element:nth-of-type(n) 指父元素下第 n 个 element 元素，element:nth-child(n) 指父元素下第 n 个元素且元素为 element，若不是，选择失败。具体细节请在使用时查找文档。

```
/* 伪类属性定义有顺序要求！ */
  a:link {
    color: gray;
  }
  a:visited {
    color:red;
  }
  a:hover {
    color: green;
    /* 鼠标悬停 */
  }
  a:active {
    color: orange;
    /* 鼠标点击 */
  }
```
### 5.2 － 其他选择器
#### 5.2.1 - 组合选择器  
- 后代选择器 .main h2 {...}，使用 表示 IE6+
- 子选择器 .main>h2 {...}，使用>表示 IE7+
- 兄弟选择器 h2+p {...}，使用+表示 IE7+
- h2~p {...}，使用~表示（此标签无需紧邻）IE7+

#### 5.2.2 - 选择器分组  
你想为html中多个标签元素设置同一个样式时，可以使用分组选择符（`，`）
```
/* 下面两组样式声明效果一致 */
h1 {color: red;}
h2 {color: red;}
h3 {color: red;}

h1, h2, h3 {color: red;}
```

---
## 6 - CSS中的继承、优先、层级
### 6.1 - 继承
CSS的某些样式是具有继承性的，那么什么是继承呢？继承是一种规则，它允许样式不仅应用于某个特定html标签元素，而且应用于其后代。比如下面代码：如某种颜色应用于p标签，这个颜色设置不仅应用p标签，还应用于p标签中的所有子元素文本，这里子元素为span标签。   
```
p{color:red;}

<p>想当年，我是一个<span>强壮</span>的男人。</p>
```
输入上面代码，p中的文本与span中的文本都设置为了红色。但注意有一些css样式是不具有继承性的。如border:1px solid red;   

子元素继承父元素的样式，但并不是所有属性都是默认继承的。通过文档中的 inherited: yes 来判断属性是否可以自动继承。  

![](https://li-xinyang.gitbooks.io/frontend-notebook/content/img/C/css-inherit-doc.png)  

自动继承属性：  
- color
- font
- text-align
- list-style
- ...

非继承属性：
- background
- border
- position
- ...

### 6.2 - 优先
有的时候我们为同一个元素设置了不同的CSS样式代码，那么元素会启用哪一个CSS样式呢?我们来看一下面的代码：  
```
p{color:red;}
.first{color:green;}
<p class="first">三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>
```
p和.first都匹配到了p这个标签上，那么会显示哪种颜色呢？green是正确的颜色，那么为什么呢？是因为浏览器是根据权值来判断使用哪种css样式的，权值高的就使用哪种css样式。

CSS Specificity Calculator 可以在[这里](http://specificity.keegan.st/)找到。更多关于 CSS 优先级别的信息可以在[这里](https://css-tricks.com/specifics-on-css-specificity/)（英文）找到。

计算方法：
- a = 行内样式
- b = id 选择器的数量
- c = 类、伪类的属性选择器的数量
- d = 标签选择器和伪元素选择器的数量
注意：从上到下优先级一次降低，且优先级高的样式会将优先级低的样式覆盖。大致公式（并不准确）如下。
`value = a * 1000 + b * 100 + c * 10 + d`


例如下面的代码：  
```
p{color:red;} /*权值为1*/
p span{color:green;} /*权值为1+1=2*/
.warning{color:white;} /*权值为10*/
p span.warning{color:purple;} /*权值为1+1+10=12*/
a,#footer .note p{color:yellow;} /*权值为100+10+1+1=112*/
```
注意：还有一个权值比较特殊--继承也有权值但很低，有的文献提出它只有0.1，所以可以理解为继承的权值最低。  

改变优先级方法:  
- 改变样式声明先后顺序
- 提升选择器优先级
- `!important`（慎用）_!important优先级样式是个例外，权值高于用户自己设置的样式。_

### 6.3 - 层叠
我们来思考一个问题：如果在html文件中对于同一个元素可以有多个css样式存在并且这多个css样式具有 **相同权重值** 怎么办？

层叠就是在html文件中对于同一个元素可以有多个css样式存在，当有相同权重的样式存在时，会根据这些css样式的前后顺序来决定，处于最后面的css样式会被应用。

如下面代码:  
```
p{color:red;}
p{color:green;}
<p class="first">三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>
```

最后 p 中的文本会设置为green，这个层叠很好理解，理解为后面的样式会覆盖前面的样式。

所以前面的css样式优先级就不难理解了：

`内联样式表（标签内部）> 嵌入样式表（当前文件中）> 外部样式表（外部文件中）。`

---
## 7 - CSS文本

### 7.1 - 字体

**7.1.1 － 改变字号**  
`font-size: <absolute-size> | <relative-size> | <length> | <percentage> | inherit`   
`<absolute-size>`有 small large medium   
`<relative-size>`有 smaller larger   
示范：  
```
  font-size 12px
  p#sample0
    font-size 16px
  p#sample1
    font-size 2em
  p#sample2
    font-size 200%
```
以上两值在开发中并不常用。2em 与 200% 都为父元素默认大小的两倍（参照物为父元素的字体大小 12px）。  

**7.1.2 - 改变字体**  
`font-family: [ <family-name> | <generic-family> ]`   
`<generic-family> `可选选项，但具体使用字体由浏览器决定    
- serif
- sans-serif
- cursive
- fantasy
- monospace

示范：  
`font-family: arial, Verdana, sans-serif;`  
注意：优先使用靠前的字体

**通用字体系列**  
一直存在混乱的字体命名问题，实际上相同的字体可能有很多不同的称呼，不过 CSS 迈出了勇敢的一步，力图帮助用户代理把这种混乱状况理清楚。

我们所认为的“字体”可能有许多字体变形组成，分别用来描述粗体、斜体文本，等等。例如，你可能已经对字体 Times 很熟悉。不过，Times 实际上是多种变形的一个组合，包括 TimesRegular、TimesBold、TimesItalic、TimesOblique、TimesBoldItalic、TimesBoldOblique，等等。Times 的每种变形都是一个具体的字体风格（font face），而我们通常认为的 Times 是所有这些变形字体的一个组合。换句话说，Times 实际上是一个字体系列（font family），而不只是单个的字体，尽管我们大多数人都认为字体就是某一种字体。

除了各种特定字体系列外（如 Times、Verdana、Helvetica 或 Arial），CSS 还定义了 5 种通用字体系列：  
* **Serif 字体**    
这些字体成比例，而且有衬线。如果字体中的所有字符根据其不同大小有不同的宽度，则成该字符是成比例的。例如，小写 i 和小写 m 的宽度就不同。
*衬线是每个字符笔划末端的装饰，比如小写 l 顶部和底部的短线，或大写 A 两条腿底部的短线*   

```
Serif 字体的例子包括
- Times
- Georgia
- New Century Schoolbook
- ...
```

* **Sans-serif 字体**   
这些字体是成比例的，而且没有上下短线，这种字体系列在计算机屏幕上更容易识读.

```
Sans-serif 字体的例子包括
- Helvetica
- Geneva
- Verdana
- Arial
- Univers
- ...
```
* **Monospace 字体**    
Monospace 字体并不是成比例的。它们通常用于模拟打字机打出的文本、老式点阵打印机的输出，甚至更老式的视频显示终端。采用这些字体，每个字符的宽度都必须完全相同，所以小写的 i 和小写的 m 有相同的宽度。这些字体可能有上下短线，也可能没有。如果一个字体的字符宽度完全相同，则归类为 Monospace 字体，而不论是否有上下短线。

```
Monospace 字体的例子包括 :
- Courier
- Courier New
- Andale Mono
- ...
```
* **Cursive 字体**  
这些字体试图模仿人的手写体。通常，它们主要由曲线和 Serif 字体中没有的笔划装饰组成。例如，大写 A 再其左腿底部可能有一个小弯，或者完全由花体部分和小的弯曲部分组成。

```
Cursive 字体的例子包括:
- Zapf Chancery
- Author
- Comic Sans
- ...
```

* **Fantasy 字体**  
这些字体无法用任何特征来定义，只有一点是确定的，那就是我们无法很容易地将其规划到任何一种其他的字体系列当中。

```
这样的字体包括 :
- Western
- Woodblock
- Klingon
- ...

```


**7.1.3 - 加粗字体**  
`font-weight: normal | bold | bolder | lighter | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900`  
示范：  
```
font-weight: normal;
font-weight: bold;
```

**7.1.4 - 倾斜字体**    
`font-style: normal | italic | oblique | inherit`  
italic 使用字体中的斜体，而 oblique 在没有斜体字体时强制倾斜字体。  

**7.1.5 - 更改行距**    
`line-height: normal | <number> | <length> | <percentage>`      
normal 值为浏览器决定，在1.1至1.2之间（通常设置值为1.14左右）
示范：  
```
/* length 类型 */
line-height: 40px;
line-height: 3em;
/* percentage 类型 */
line-height: 300%;
/* number 类型 */
line-height: 3;
```
注意：当line-height为 number 类型时，子类直接继承其数值（不计算直接继承）。 而当为 percentage 类型时，子类则会先计算再显示（先计算后继承）。  

**7.1.6 - 字间距（字母间距）**   
`letter-spacing: normal | <length>`
其用于设置字间距或者字母间距，此属性适用于中文或西文中的字母。 如果需要设置西文中词与词的间距或标签直接的距离则需要使用 word-spacing。`word-spacing: normal | <length>`

**7.1.7 - 改变文字颜色**  
`color: <color>`  
示范：  
```
element { color: red; }
element { color: #f00; }
element { color: #ff0000; }
element { color: rgb(255,0,0); }
element { color: rgb(100%, 0%, 0%); }
element { color: hsl(0, 100%, 50%); }

/* 50% translucent */
element { color: rgba(255, 0, 0, 0.5); }
element { color: hsla(0, 100%, 50%, 0.5); }

/* 全透明 */
element { color: transparent' }
element { color: rgba(0, 0, 0, 0); }
```

### 7.2 - 对齐方式

**7.2.1 - 文字居中**        

`text-align: start | end | left | right | center | justify | match-parent | start end`  
注意：默认为文本左对齐。

**7.2.2 - 文本垂直对齐**      
`vertical-align: baseline | sub | super | text-top | text-bottom | middle | top | bottom | <percentage> | <length>`
注意：`<percentage>`的参照物为line-height   

**7.2.3- 文本缩进**     
`text-indent: <length> | <percentage> && [ hanging || each-line ]`  
注意：缩进两个字可使用 text-indent: 2em;   

### 7.3 - 格式处理

**7.3.1 - 保留空格格式**      
`white-space: normal | pre | nowrap | pre-wrap | pre-line`
注意：`pre `行为同 `<pre>` 一致。

|          | New lines | Spaces and tabs | Text wrapping |
|:---------|:----------|:----------------|:--------------|
| normal   | Collapse  | Collapse        | Wrap          |
| nowrap   | Collapse  | Collapse        | No wrap       |
| pre      | Preserve  | Preserve        | No wrap       |
| pre-wrap | Preserve  | Preserve        | Wrap          |
| pre-line | Preserve  | Collapse        | Wrap          |

**7.3.2 - 文字换行**    
`word-wrap: normal | break-word`        
注意：允许长单词自动换行。
`word-break: normal | break-all | keep-all`
注意：`break-all` 单词中的任意字母间都可以换行。

### 7.4 - 文本装饰

**7.4.1 - 文字阴影**    
`text-shadow:none | <shadow-t># `或 `text-shadow:none | [<length>{2,3}&&<color>?]#`

```
p {
  text-shadow: 1px 1px 1px #000,
               3px 3px 5px blue;
}
```
- value = The X-coordinate X 轴偏移像素
- value = The Y-coordinate Y 轴偏移像素
- value = The blur radius 阴影模糊半径
- value = The color of the shadow 阴影颜色（默认为文字颜色）

**7.4.2 - 文本装饰（下划线等）**  
`text-decoration: <'text-decoration-line'> || <'text-decoration-style'> || <'text-decoration-color'>`

```
h1.under {
    text-decoration: underline;
}
h1.over {
    text-decoration: overline;
}
p.line {
    text-decoration: line-through;
}
p.blink {
    text-decoration: blink;
}
a.none {
    text-decoration: none;
}
p.underover {
    text-decoration: underline overline;
}
```

### 7.5 － 高级设置

**7.5.1 - 省略字符**    
`text-overflow: [ clip | ellipsis | <string> ]{1,2}`    

```
/* 常用配合 */
text-overflow: ellipsis;
overflow: hidden; /* 溢出截取 */
white-space: nowrap; /* 禁止换行 */
```

**7.5.2 - 更换鼠标形状**  
```
cursor: [[<funciri>,]* [ auto | crosshair | default | pointer | move | e-resize | ne-resize | nw-resize | n-resize | se-resize | sw-resize | s-resize | w-resize| text | wait | help ]] | inherit+
```
常用属性    
`cursor: [<uri>,]*[auto | default | none | help | pointer | zoom-in | zoom-out | move]`
- `<uri>` 图片资源地址代替鼠标默认形状
- `<default>` 默认光标
- `<none>` 隐藏光标
- `<pointer>` 手型光标
- `<zoom-in>`
- `<zoom-out>`
- `<move>`

示范：
```
cursor: pointer;
cursor: url(image-name.cur), pointer;
/* 当 uri 失效时或者则会起作用 */
```

**7.5.3 - 强制继承**
`inherit` 会强制继承父元素的属性值。
```
font-size: inherit;
font-family: inherit;
font-weight: inherit;
...
word-wrap: inherit;
work-break: inherit
text-showdow: inherit
```
