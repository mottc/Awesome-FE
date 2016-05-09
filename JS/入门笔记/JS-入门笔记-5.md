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

## 属性访问错误
查询一个不存在的属性并不会报错，如果对象自身的属性和继承的属性中均没有，则会返回undefined。

但是如果对象不存在，试图查询这个不存在的对象的属性就会报错。null和undefined都没有属性，因此查询这些值的属性会报错

下面提供2种避免出错的方法：
```
// 简单的方法
var len = undefined;
if(book){
  if(book.title) len = book.title.length;
}
// 更为灵活的方法
var len = book && book.title && book.title.length; // &&短路行为
```

给null和undefined设置属性会报类型错误

给其他值设置属性不会全部成功，有一部分属性是只读的，不能重新赋值，有一些对象不能新增属性，但是这些设置属性的失败操作不会报错。但在ECMAScript5的严格模式下会报异常
```
Object.prototype = o; // 失败，Object.prototype没有被修改
```

总之，下面场景中给对象o设置属性p会失败：
- o的属性是只读的，不能给只读的属性重新赋值
- o中的属性p是继承属性，且它是只读的，不能通过同名自有属性覆盖只读的继承属性
- o中不存在自有属性p：o没有使用setter方法继承属性p，并且o的可扩展性是false。如果o中不存在p，且没有setter方法可以调用，则p一定会添加到o中，但如果o不是可扩展的，那么在o中不能定义新属性

## 删除属性
delete运算符可以删除对象的属性。但是，delete只是断开属性和宿主对象的联系，不是删除这个属性。因此，在销毁对象的时候，要遍历属性中的属性，依次删除
```
a = { p: {x:1}}; //
b = a.p; // b是对a的属性p的一个引用
delete a.p; // 删除a的属性p
b.x; // => 1，已经删除的属性p的引用仍然存在
```

delete运算符只能删除自有属性，不能删除继承属性。

当delete表达式删除成功后并且没有副作用，返回true。如果delete后面不是一个属性访问表达式，同样返回true
```
o = {x:1};
delete o.x; // 删除x，true
delete o.x; // 删除失败，什么都不做，返回true
delete o.toString(); // 无法删除，返回true
delete 1; // 无意义，返回true
```

delete 可以删除不可扩展对象的可配置属性，但不能删除可配置性为false的属性。在严格模式中，删除一个不可配置的属性会报一个类型错误。
在非严格模式下，这些情况delete操作会失败并返回false:
```
delete Object.prototype; // 不能删除，属性不可配置
var x=1; // 声明一个全局变量
delete this.x; // 不能删除这个属性
function f(){}; // 声明一个全局函数
delete this.f; // 也不能删除全局函数
```

当在非严格模式中删除全局对象的可配置属性时，可以省略对全局对象的引用，直接delete后面跟要删除的属性名即可：
```
this.x = 1;
delete x;
```

在严格模式中，delete后跟随一个非法的操作数，将会报一个语法错误。必须显式的指定对象及其属性。
```
delete x; // 严格模式下报语法错误
delete this.x; // 正常
```

## 检测属性

我们经常需要判断一个属性是否存在某个对象中。
- in运算符
- hasOwnPreperty()
- propertyIsEnumerable()

in运算符左侧是属性名，右侧是对象，如果对象的自有属性或继承属性包含这个属性，返回true
```
var o = {x:1};
"x" in o; // true，“x”是o的属性
"y" in o; // false， 'y'不是o的属性
"toString" in o; // true，o继承toString属性
```

对象的hasOwnPreperty()方法用来检测给的的名字是否是对象的自有属性。对于继承属性返回false
```
var o = {x:1};
o.hasOwnPreperty("x"); // true,o有一个自有属性x
o.hasOwnPreperty("y"); // false，o没有属性y
o.hasOwnPreperty("toString"); // false，toString是继承的属性
```

propertyIsEnumerable()是hasOwnPreperty()的增强版，只有检测到是自有属性且这个属性的可枚举性为true时，才会返回true。
某些内置属性是不可枚举的。通常js代码创建的属性都是可枚举的，除非在ECMAScript5中使用一个特殊的方法来改变属性的可枚举性。
```
var o =inheritPrototype({y:2});
o.x = 1;
o.propertyIsEnumerable("x"); // true，o有一个可枚举的属性x
o.propertyIsEnumerable("y"); // false，y属性是继承来的
object.prototype.propertyIsEnumerable("toString"); // false， 不可枚举的
```

除了使用in运算符之外，另一种更简便的方法是使用`!==`判断一个属性是否是undefined:
```
var o = {x:1};
o.x !== undefined; // true，o中有属性x
o.y !== undefined; // false，y属性没有
o.toString !== undefined; // true，o继承了toString
```

然后有一种情况，只能用in运算符，不能使用上述属性访问表达式。in运算符可以区分不存在的属性和存在但值为undefined的属性。
```
var o = {x:undefined};
o.x !== undefined; // false,属性存在，但是值为undefined
o.y !== undefined; // false，属性不存在
"x" in o; // true，属性存在
"y" in o; // false，属性不存在
delete o.x; // 删除属性x
"x" in o; // 属性x不存在
```
注意，上面使用的是`!==`而不是`!=`,`!==`可以区分undefined和null。有时不需要进行区分：
```
// 如果o中含有属性x，且x值不是null或undefined
if (o.x != null) o.x += 2;
// 如果o中含有属性x，且x的值不能转换成false，乘以2
// 如果x是undefined、null、false、" "、0 或者NaN，则保持不变
if (o.x) o.x *= 2;
```

## 枚举属性
除了检测对象的属性是否存在，还经常需要遍历对象的属性。通常使用for/in循环遍历

for/in循环可以遍历对象中所有可枚举的属性（包括自身和继承的属性）

一般来说，对象继承的内置方法是不可枚举的，还有通过Object.defineProperty(obj,property,enumerable:false)来定义不可枚举的属性
```
var o = { x:1, y:2}; // 2个可枚举的属性
o.propertyIsEnumerable("toString"); // false 继承的方法，不可枚举
for(p in o){
  console.log(p)  // 输出x,y，不会输出toString
}
```

很多时候给对象添加新的方法或属性，但是会被for/in枚举，因此需要跳过继承的属性和跳过方法，来避免在for/in中被循环枚举出来
```
for(p in o){
  if(!o.hasOwnPreperty(p)) continue;
}
for(p in o){
  if(typeof o[p] === "function") continue;
}
```

除了for/in循环之外，ECMAScript5定义了2个用来枚举属性名称的函数
- Object.keys()，返回一个数组，数组由对象中可枚举的自有属性的名称组成
- Object.getOwnPropertyNames()，与keys相似，但是它返回所有自有属性的名称，而不仅仅是可枚举的属性

## 属性getter和setter
对象属性是由名字、值和一组特性(attribute) 构成的。

在ECMAScript5中，属性可以用1-2个方法替代，这两个方法就是getter和setter。

由getter和setter定义的属性称作“存取器属性”(access property)，与“数据属性”不同，数据属性只有一个简单的值。

当程序查询存取器属性的值时，js调用getter方法（无参数），这个方法返回值就是属性存取表达式的值。
当程序设置一个存取器属性的值时，js调用setter方法，将赋值表达式右侧的值当作参数传入setter。可以忽略setter方法的返回值。

和数据属性不同，存取器属性不具有可写性(writable attribute)。如果属性同时具有getter和setter方法，那么是一个读/写属性，
如果它只有getter方法，那么它是一个只读属性；如果它只有setter方法，那么它是一个只写属性，读取只写属性，只会返回undefined

定义存取器最简单的方法如下：
```
var o = {
  // 普通的数据属性
  data_prop: value;

  // 存取器都是成对定义的函数
get accessor_prop() { /* function body */ }
set accessor_prop(value) { /* function body */ }
}
```

注意，存取器属性定义为1个或者2个和属性同名的函数，但是没有使用function，而是使用get和set。

来看个例子：表示2D笛卡尔坐标系的对象
```
var p = {
  // 2个普通的读写属性
  x: 1.0,
  y: 1.0,

  // r是可读写的存取器属性，有getter和setter
  // 函数体结束后，不要忘记加逗号
  get r() { return Math.sqrt(this.x*this.x + this.y*this.y); }
  set r(newvalue) {
    var oldvalue = Math.sqrt(this.x*this.x + this.y*this.y);
    var ratio = newvalue/oldvalue;
    this.x *= ratio;
    this.y *= ratio;
  }

  // theta是只读存取器，只有getter
  get theta() { return Math.atan2(this.y, this.x); }
}
```
注意，在这段代码中，getter和setter中this关键字的用法。js把这些函数当作对象的方法来调用，也就说，在函数体内的this指向表示这个点的对象，
因此，r属性的getter方法可以通过this.x和this.y引用x和y的属性。

和数据属性一样，存取起属性是可以继承的，因此可以将上述代码的对象p当在另一个点的原型。可以给新对象定义它的x和y属性，但r和theta属性是继承的：
```
var q = inheritPrototype(p); // 创建一个继承getter和setter的新对象
q.x = 1, q.y = 2; // 给q添加2个属性
console.log(q.r); // 可以使用继承的存取器属性
console.log(q.theta);
```
