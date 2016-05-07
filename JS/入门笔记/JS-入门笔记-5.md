# 对象

对象(object)是js的基本数据类型。是一种复合值：将很多值（原始值或者其它对象）聚合在一起，可以通过名字访问这些值。
每个属性都是一个名/值对(key/value)，属性名是字符串，因此我们可以把对象看成从字符串到值的映射。
然而对象不仅仅是字符串到值的映射，除了保持自有的属性，js对象还可以从一个称为原型的对象继承属性。
对象的方法通常是继承的属性，这种原型式继承是js的核心特征。

js对象是动态的，可以新增属性，也可以删除属性。

除了字符串、数字、true、false、null和undefined之外，js中的值都是对象。

对象是可变的，我们通过引用而非值来操作对象。如果变量x是指向一个对象的引用，那么执行代码
`var y = x;`变量y也是指向同一个对象的引用，而非这个对象的副本。通过y来修改这个对象也会对变量x造成影响

js的属性，除了名字和值之外，每个属性还有一些与之相关的值，称为 **属性特性**：
- 可写，表明是否可以设置该属性的值
- 可枚举，表明是否可以通过for/in循环返回该属性
- 可配置，表明是否可以删除或修改该属性

除了包含属性之外，每个对象还拥有三个相关的对象特性：
- 对象的原型(prototype)指向另一个对象，本对象的属性继承自它的原型对象
- 对象的类是一个标识对象类型的字符串
- 对象的扩展标记(extensible flag)指明了在ECMAScript5中是否可以向该对象添加新的属性

三类js对象和两类属性的区分：
- 内置对象(native object)是由ECMAScript规范定义的对象或类。例如，数组、函数、日期和正则表达式
- 宿主对象(host object)是由js解释器所嵌入的宿主环境（比如WEB浏览器）定义的。客户端js中表示网页结构的HTMLElement对象均是宿主对象。既然宿主环境定义的方法可以当成普通的js函数对象，那么宿主对象也可以当成内置对象
- 自定义对象(user-defined Object)是由运行中的js代码创建的对象
- 自有属性(own property)是直接在对象中定义的属性
- 继承属性(inherited property)是在对象的原型对象中定义的属性

## 创建对象
创建对象主要有三种方法:
- 对象直接量
- 关键字new创建
- Object.create()函数

### 对象直接量
对象直接量是由若干名值对组成的映射表，名值对中间用冒号分割，名值对之间用逗号分割，整个映射表用花括号括起来

属性名可以是js标识符也可以是字符串直接量

属性的值可以是任意类型js表达式、表达式的值就是这个属性的值

来个例子：
```
var empty = {}; // 没有任何属性的对象
var point = { x:0, y:1 }; // 两个属性
var point2 = { x: point.x; y: point.y }; // 更复杂的属性值
var book = {                
  "main title": "javascript", // 属性名字有空格，必须用字符串表示
  "sub-titile": "book", // 属性名字有连字符，必须用字符串表示
  "for": "all audience", // 属性名字是保留字，必须用引号
  author: {               // 允许的名字可以没有引号
    firstname: "zhao",
    subname: "lion"
  }
}
```

对象直接量是一个表达式，这个表达式的每次运算都创建并初始化一个新的对象。每次计算对象直接量时候，也都会计算它的每一个属性的值。

### 通过new创建对象
new 运算符创建并初始化一个新对象。关键字new后跟随一个函数调用。这个函数被称为 **构造函数(constructor)**
构造函数用来初始化一个新创建的对象。js语言核心中原始类型都包含内置构造函数.比如:
```
var o = new Object(); // 创建一个空对象
var a = new Array(); // 创建一个空数组
var d = new Date(); // 创建一个当前时间对象
var r = new RegExp("^js"); // 创建一个可以进行模式匹配的RegExp对象
```
### 原型
每一个js对象(null除外)都和另一个对象相关联。“另一个对象”就是我们经常听到的原型，每一个对象都从原型继承属性。

所有通过对象直接量创建的对象都具有同一个原型对象，并且可以通过`Object.prototype`来获得原型对象的引用。

通过new创建和构造函数调用创建的对象原型就是构造函数的prototype属性的值。因此，同使用{}创建对象一样，通过new Object()创建的对象也继承自Object.prototype。
同样，通过new Array()创建的对象原型就是Array.prototype，通过new Date()创建的对象的原型就是Date.prototype。

没有原型的对象为数不多，Object.prototype就是一个。它不继承任何属性。

其它原型对象都是普通对象，普通对象都有原型。所有的内置构造函数（以及大部分自定义构造函数）都具有一个继承自Object.prototype的原型。而这一系列的原型对象就是所谓的“原型链”

### Object.create()
ECMAScript5定义了一个`Object.create()`的方法,创建一个新对象，其中一个参数就是这个对象的原型。Object.create()提供第二个可选参数，用以对新对象的属性进行进一步描述.

语法如下：
`Object.create(proto[, propertiesObject])`

Object.create()是一个静态函数，不是提供给某个对象调用的方法。使用很简单，传入所需的原型对象即可:
```
var o1 = Object.create({ x:1, y:2}); // o1继承属性x和y
```

可以通过传入参数null来创建一个没有原型的新对象。通过这种方式创建的对象不会继承任何东西，包括toString()
```
var o2 = Object.create(null); // o2不继承任何属性和方法
```

如果想创建一个普通的空对象（类似通过{}或new Object()创建的对象)，需要 Object.prototype：
```
var o3 = Object.create(Object.prototype); // o3和{}和new Object()创建对象一样
```

可以通过任何原型创建新对象。但是如果遇到js实现不支持Object.create()时，如何模拟原型继承呢？看下代码:
```
function inheritPrototype(p){
  if(p==null) throw TypeError(); // p是一个对象，不能是null
  if(Object.create)  // 如果存在Object.create方法，使用
    return Object.create(p);
  var t = typeof p;  // 否则进一步检测
  if(t !== "object" && t !== "function") throw TypeError(); // 如果既不是对象，也不是函数，抛出异常
  function f() {}; // 定义一个空构造函数
  f.prototype = p; // 将原型指向p
  return new f(); // 使用f()创建p的继承对象
}
```

上面这个函数模拟了一部分Object.create一部分，但还是非常有用的。比如防止库函数无意间修改不受你控制的对象。
不是将对象直接作为参数传入函数，而是将它的继承对象传入函数。当函数读取继承对象的属性时，实际上读取的事继承来的值。
如果给继承对象的属性赋值，则这些属性之后影响这个继承对象自身，不会影响原始对象：

```
var o = {x: "don't change this value"}; //  创建一个对象
var inherit_o = inheritPrototype(o); // 创建一个原型是o的继承对象
inherit_o.x = "change it"; // 修改继承对象本身的属性x
o.x; // => "don't change this value" 原型o的属性并没改变
```

## 属性的查询和设置
查询属性可以通过`.` 和`[]`来获取属性的值。
- `.`的右侧必须是一个以属性名称命名的简单标示符
- `[]`的方括号内必须是一个计算结果为字符串的表达式

```
var author = book.author;
var name = author.subname;
var title = book["main title"]
```

和查询属性一样，可以通过`.` 和`[]`来获取创建属性或给属性赋值。
```
book.edition = 1;
book["main title"] = "Js";
```

当通过[]访问对象属性时，可以在程序运行时修改和创建。举个例子：    
通过读取customer对象的address0/address1/address2的属性，并且连接起来
```
var addr = "";
for(var i=0; i<3; i++){
  addr += customer["address"+i] + '\n';
}
```

## 继承

js对象具有自己的属性，也有一些属性从原型对象继承而来。

假如要查询对象o的属性x，如果o中不存在x，那么将会在o的原型中查询属性x。如果原型对象也没有x，但是这个原型对象也有原型，
那么继续在这个原型对象的原型上查询，直到找到x或者查找到一个对象的原型是null为止。

这样对象的原型属性构成一个“链”，通过这个”链实现属性的继承。

看看下面这个栗子，加强一下理解：
```
var o = {}; // 创建一个空对象
o.x = 1; // o对象新增一个属性x
var p = inheritPrototype(o); // 上面提到的继承函数，p继承自o
p.y = 2; // p新增一个属性y
var q = inheritPrototype(p); // q继承自p
q.z = 3; // q新增属性z
var s = q.toString(); // toString继承自Object.prototype
q.x + q.y; // x继承自o，y继承自p
```

**在属性赋值上，总是在原始对象上去创建属性或对已有的属性赋值，不会修改原型链**

只有查询属性，才会体会继承的存在，而设置属性与继承无关，这是js的重要特性，务必记住

这种特性，让程序员有选择的覆盖继承的属性:
```
var raw_circle = { r:1 };
var new_circle = inheritPrototype(raw_circle); // new_circle继承自raw_circle
new_circle.r = 2; // 修改new_circle继承来的属性的值，只修改自身
raw_circle.r; // => 1 ,原型的值并没有改变
```

### 属性访问错误
