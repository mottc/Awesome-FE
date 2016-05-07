# 语句

js程序其实就是一系列可执行语句的集合。只要掌握了语句，就可以开始写js程序

默认情况下，js依照语句编写顺序依次执行，其中有很多语句和控制语句，来改变默认执行顺序:
- 条件语句，js解释器根据一个表达式的值来判断是执行还是跳过这些语句，比如`if`语句、`switch`语句
- 循环语句，可以重复执行语句，如`while`语句和`for`语句
- 跳转语句，可以让解释器跳转至程序的其他部分继续执行，如`break`语句、`return`语句、 `throw`语句

## 表达式语句

- 赋值语句
- 递增、递减运算符
- 函数调用

```
greeting = "hello" + name;
i *= 3;

counter++;

delete o.x;

window.close();

cx = Math.cos(x);
```

## 复合语句和空语句

js可以讲多条语句联合在一起，形成一条复合语句，只需要用花括号将多条语句括起来即可。

下面代码可以当成一条单独的语句，使用在任何js希望使用一条语句的地方：
```
{
  x = Math.PI;
  cx = Math.cos(x);
  console.log("cos(pi) = " + cx);
}
```

关于语句块，需要注意:
- 语句块结尾不需要分号，块中语句必须以分号结束，但语句块不需要
- 语句块中的缩进不是必须的，但是为了代码可读性，还是需要整齐的缩进更好
- js中没有快级作用域，语句块中声明的变量并不是语句块私有的

在js中，希望多条语句被当作一条语句使用时，使用复合语句来替代，空语句正好相反，允许包含0条语句
空语句如下:
```
;
```
js执行空语句时，不会执行任何动作。但是创建一个具有空循环体时，空语句很有用
```
for(var i=0; i<a.length; a[i++]=0) ;
```

注意，在for循环、while循环或if语句的右圆括号后的分号不起眼，很容易造成一些不容易定位的bug
```
if((a == 0) || ( b == 0)); // 这一行代码没有执行任何东西
o = null;    // 这一行总会执行
```

**如果有特殊目的需要使用空语句，最好在代码中注释**

## 声明语句

`var`和`function`都是声明语句，它们声明或定义变量或函数。

### var
`var` 语句用来声明一个或多个变量。关键字var后面跟随的是要声明的变量列表，每个变量都可以带有初始化表达式，用于指定初始值

栗子：
```
var i;
var j = 0;
var p,q;
var greeting = "hello" + name;
var x = 2.34,y = Math.cos(1), r, theta;
var x = 2,
    f = function(x) { return x*x;},
    y = f(x);
```

如果var语句出现在函数体内，那么定义的是一个局部变量，作用域就是这个函数。

如果在顶层代码中使用var语句，那么声明的是一个全局变量，在整个js程序都是可见的

var声明的变量是无法通过delete删除的

如果var语句中的变量没有指定初始化值，那么这个变量的值初始化为undefined

### function
关键字`function`用来定义函数，例如以下函数定义表达式形式写法来定义函数：
```
var f = function(x) { return x*x; };
function f(x) { return x+1; };
```

大括号包起来的是函数体，函数体是由js语句组成的，语句数量不限。

在定义函数时，并不执行函数体内的语句，它和调用函数时的新函数对象相关联。

注意即使只有一条语句，也需要用花括号包起来。    
下面是一些函数声明形式的栗子：
```
function hypotense(x,y) {
  return x*x + y*y;
}
```

函数声明语句通常出现在js代码的最顶层，也可以嵌套在其它函数体内。但是嵌套函数定义时，注意函数声明只能出现在所嵌套函数顶部
不能出现在if语句、while循环或其他任何语句中

函数声明语句和函数定义表达式的不同:
- 函数声明语句中的函数名是一个变量名，变量指向函数对象。和通过var声明变量一样，函数定义语句的函数被显式的“提前”到了脚本或函数的顶部，在整个脚本和函数内是可见的
- 使用var的话，只有变量名被提前了，变量初始化代码仍然在原来的位置。使用函数声明语句的话，函数名称和函数体均被提前。

和var语句一样，函数声明语句创建的变量是无法删除的。

## 条件语句

js中基本的条件语句有`if/else`语句和`switch`语句

### if语句

主要有3种形式
- `if ...`
- `if...else...`
- `if...else if...else...`


**`if ...`**
```
if (exoression)
  statement;
```

**`if...else...`**
```
if (expression)
  statement1;
else
  statement2;
```

**`if...else if...else...`**
```
if (expression1)
  statement1;
else if(expression2)
  statement2;
else
  statement3;
```

### switch语句

如果所有的程序执行分支都依赖于同一个表达式时，if-else并不是最佳解决方案，而switch语句正适合处理这种情况

```
switch(n): {
  case 1:
    // 执行代码块1
    break;
  case 2:
    // 执行代码块2
    break;
  case 3:
    // 执行代码块3
    break;
  default:
    // 执行代码块4
    break;
}
```

由于switch语句每次执行时候，不是所有的case表达式都能执行，因此，应当避免使用带有副作用的case表达式，
最安全的做法是case中使用常量表达式

## 循环语句
js中有4中循环语句，`while`,`do/while`,`for`,`for/in`

### while语句

while 语句基本语法如下:   
```
while(expression)
  statement
```

执行while之前，js解释器先计算expression值，如果值是假的，那么程序将跳过循环体中的逻辑。反之，js将执行循环体内的逻辑，
然后再次计算表达式expression的值，这种循环会一直下去，直到expression值为假值为止。

下面这个示例演示while循环输出0-9:     

```
var count = 0;
while( count < 10 ){
  console.log(count++);
}
```

### do/while语句

do/while语句和while语句非常接近，只不过检测循环表达式是在循环结束时候，也就说至少执行一次

```
do {
  statement
}while(expression)
```

下面是一个do/while循环的栗子：
```
var count = 0;
do {
  console.log(count++)
}while(count<10)
```

### for语句

大部分循环都有特定的计数变量，在循环开始之前，初始化这个变量，然后每次循环执行之前都检测一下他的值，最后，
计数器变量做自增操作。

在这类循环中，计数器的三个关键操作是：初始化、检测、更新

for语句将这三步操作明确声明为循环语法一部分，各自使用一个表达式来表示。

for语句的语法如下：
```
for(initialize; test; increment;){
  statement
}
```

initialize,test,increment三个表达式之间用分号分割，分别负责初始化操作，循环条件判断和计数器变量更新。

for循环输出0-9的栗子：
```
for(var count=0; count<10;count++){
  console.log(count);
}
```

### for/in语句
for/in语句和常规for循环完全不同。语法如下：
```
for(variable in object){
  statement
}
```

variable 通常是一个变量名，也可以是一个产生左值的表达式或者一个通过var语句声明的变量，总之必须是一个适合赋值
表达式左侧的值。object是一个表达式，这个表达式计算结果是一个对象。

for循环遍历数组元素是非常简单的，for/in循环更适合用来遍历对象属性成员

```
for(var p in o){
  console.log(o[p])
}
```

需要注意的是，只要for/in循环中，variable的值可以当作赋值表达式的左值，它可以是任意表达式。每次循环都会计算这个表达式，
也就是说，每次循环他计算的值都有可能不同。

例如，可以使用下面这段代码将所有对象属性复制到一个数组中
```
var o = {x:1,y:2};
var a=[],i=0;
for(a[i++] in o) ; /*empty*/
```

js数组不过是一种特殊的对象，因此，for/in循环可以像枚举对象属性一样，枚举数组索引。

例如可以在上面代码之后加上这段代码，可以枚举数组的索引0,1,2：
```
for(i in a) console.log(i);
```

其实，for/in循环并不会遍历对象的所有属性，只有可枚举的属性才会被遍历到。由js语言核心定义的内置方法就不是可枚举的.
除了内置方法之外，还有很多内置对象的属性也是不可枚举的。

代码中定义的所有属性和方法都是可枚举的。

对象可以继承其他对象的属性，那些继承的自定义属性也可以使用for/in枚举出来

**属性枚举的顺序：**    
规范没有指定for/in循环按照何种顺序来枚举对象属性，实际上主流浏览器厂商的js实现是按照属性定义的先后顺序来枚举简单对象的属性：
**先定义，先枚举**

## 跳转语句

js中有一类语句是跳转语句。从名字就能看出，这种语句就是使得js的执行可以从一个位置跳转到另一个位置。

- break语句是跳转到循环或者其它语句的结束
- continue语句是终止本次循环的执行并开始下一次循环的执行。
- 跳转到语句标签位置
- return语句让解释器跳出函数体执行，并提供本次调用的返回值
- throw语句触发或者抛出一个异常，配合try/catch/finally语句一同执行，跳转到最近的闭合异常处理程序

### 标签语句
语句是可以加标签的，标签由语句前的标示符和冒号组成` identifier: statement`

通过给语句定义标签，就可以在程序的任何地方通过标签名引用这条语句。break和continue是js唯一可以使用语句标签
的语句.      

用作标签的identifier 必须是一个合法的js标识符，不能是保留字

标签的命名空间和变量或函数的命名空间是不同的，因此可以使用同一个标示符作为语句标签和作为变量名或者函数名。

一个语句标签不能和它内部的语句标签重名，但在两个代码段不互相嵌套时候，是可以出现同名语句标签。并且带有标签的语句
还可以带有标签，任何语句都可以有多个标签

比如下面这个栗子，while循环定义一个标签，continue使用这个标签:
```
mainloop: while(token != null ){
  statement1;
  continue mainloop; // 跳转到下一次循环
  statement2;
}
```

### break语句

单独使用break语句的作用是立即退出最内层的循环或者switch语句。`break;`

由于它能够使循环和switch语句退出，因此这种形式的break只有出现在这类语句中才是合法的。

在switch中已经见过break的用法，在循环中，无论什么原因，只要不想执行整个循环，就可以使用break来退出

例如下面这个栗子，找到了需要查找的数组元素，就使用break退出

```
for(var i=0; i<a.length; i++){
  if(a[i] == target) break;
}
```

js同样运行break后面跟一个语句标签：`break labelname;`

当break和标签一块使用时候，程序跳转到标签所标示的语句块的结束，或者直接终止这个闭合语句块的执行。
当没有任何语句块指定了break所用的标签，将会产生一个语法错误

当使用带标签形式的break语句，带标签的语句不该是循环或者switch语句，因为break会跳出任何闭合的语句块。

在break和labelname之间不能换行。因为js可以给语句自动补全省略掉分号，如果break关键字和标签之间有换行，
js会认为你使用break不带标签的形式，会在break后补充分号

当你希望通过break跳出非就近的循环体或者switch语句，就会用到带标签的break语句。比如下面这个栗子：
```
var matrix = getData() // 得到一个二维数组
var sum=0, success = false;
compute_sum: if(matrix) {
  for(var x=0; x<matrix.length; x++){
    var row = matrix[x];
    if(!row) break compute_sum;
    for(var y=0; y<row.length; y++){
      var cell = row[y];
      if(isNaN(cell)) break compute_sum;
      sum += cell;
    }
  }
}
```
最后，不管break语句带不带标签，他的控制权都无法越过函数边界。比如，对于一条带标签的函数定义语句来说，不能
从函数内部通过这个标签跳转到函数外部

### continue语句

continue语句和break语句非常接近，但是不退出循环，而是执行下一次循环。

continue语法非常简单:`continue`

continue语句同样可以带有标签:`continue labelname`

不管continue语句带不带标签，只能在循环体中使用，在其他地方使用，会报语法错误

当执行到continue语句时候，当前循环逻辑就终止了，随即执行下一次循环，在不同类型循环中，continue行为也有些不同：
- while循环，在循环开始处指定的expression会重复检测，如果检测结果为true，循环体从头开始执行
- do/while循环，程序的执行直接跳到循环结尾处，这时会重新判断循环条件，之后再继续下一次循环
- for循环中，首先计算自增表达式，然后再次检测test表达式，以判断是否继续执行循环
- for/in语句中，循环开始访问下一个属性名，这个属性名赋给指定的变量

需要注意的是，continue语句在while和for循环中差别，while循环直接进入下一轮的循环条件判断，但for
循环首先计算自增表达式，然后判断循环条件。

下面这个栗子，展示产生一个错误时候跳过当前循环后续的逻辑：
```
for(var i=0; i<data.length; i++){
  if(!data[!]) continue;
  total += data[i];
}
```

和break语句类似，带标签的continue语句可以嵌套在循环中，用以跳出多层次嵌套循环体逻辑。同样的，在continue和labelname之间不能换行。

### return 语句

函数调用是一种表达式，而所有的表达式都有值。函数中的return语句就是用来指定函数调用后的返回值

return语句的语法:`return expression`

return语句只能在函数体内出现，如果不是将会报语法错误。当执行到return语句时，函数终止执行，返回expression的值

举个栗子:
```
function square(x) { return x*x; }
square(2)
```

如果没有return语句，则函数调用仅依次执行函数体内的每一条语句直到函数结束，最后返回调用程序。
这种情况下，调用表达式的结果是undefined。

return语句常作为最后一条语句出现，但不一定是放到函数最后，即使在执行return语句的时候后续还有很多代码
没有执行，函数还是会返回调用程序

return 语句可以单独使用而不必带有exoression，这样函数调用返回的也是undefined

### throw语句

异常，就是发生了某种异常情况或错误时产生的一种信号。    
抛出异常，就是用信号通知发生了错误或异常情况。   
捕获异常，就是处理这个信号，采取必要的措施从异常中恢复。

js中，产生运行错误或者使用throw语句时就会显式的抛出异常。使用try/catch/finally语句可以捕获异常

throw语句的语法:`throw expression;`

expression的值可以是任意类型的，可以抛出一个代表错误码的数字，或者可读的错误消息的字符串。

js解释器抛出异常时，通常采用Error类型和其子类型。

一个Error对象有一个name属性表示错误类型，一个message属性用来存放传递给构造函数的字符串。

下面看个栗子，用非法参数调用函数时抛出一个Error对象
```
function factorial(x){
  // 如果输入参数是非法的，则抛出一个异常
  if (x < 0) throw new Error("X 不能是负数");
  // 否则计算一个值，并返回
  for(var f = 1;x > 1; f *= x, x--) /*empty*/
}
```

当抛出异常时，js解释器会立即停止当前正在执行的逻辑，并跳转到就近的异常处理程序。异常处理程序就是
try/catch/finally语句编写的。    
如果抛出异常的代码块没有一条相关联的catch语句块，js解释器会从更高层的闭合代码块，查看是否有关联的
catch从句，直到找到一个异常处理程序为止。   
如果抛出的异常没有相关的异常处理函数，异常会向上传播到调用该处的
函数的代码，异常就会沿着js方法的词法结构和调用栈向上传播，没有任何异常处理程序，js把异常当作程序错误来处理，
并报告给用户。

### try/catch/finally语句
try／catch/finally语句是js的异常处理机制。
- try从句定义了需要处理的异常所在的代码块，
- catch从句跟在try之后，当try语句块内发生异常，调用catch内的代码逻辑。
- finally语句跟在catch之后，放置清理代码，不管是否发生异常，finally代码块的逻辑总是会执行。

try之后跟随atch、finally语句块可以二者只选一个，组成配合语句。

下面代码说明了，try/catch/finally的语法和使用目的

```
try{
  // 通常来讲，这里的代码从头到尾执行不会产生任何问题
  // 但有时抛出一个异常，要么是throw语句直接抛出异常，
  // 要么是通过一个方法间接抛出异常
}
catch(e){
  // 当且仅当try语句抛出异常，才会执行这里的代码
  // 这里通过局部变量e可以获得对Error对象或者抛出的其他值的引用
  // 还可以通过throw语句重新抛出异常
}
finally{
  // 不管是否抛出异常，这里的逻辑都会执行，终止try语句块的方式有
  // 1. 正常终止，执行完语句块最后一条语句
  // 2. 通过break/continue/return语句终止
  // 3. 抛出一个异常，异常被catch从句捕获
  // 4. 抛出一个异常，异常未被捕获，继续向上传播
}
```

## 其它语句类型
js最后还有三种语句类型：with,debugger 和use strict

### with语句
之前讲解全局变量时了解过一些作用域链的问题，with语句就是用来临时扩展作用域链。语法如下：
```
with(object)
statement
```

这条语句将object添加到作用域链头部，然后执行statement，最后把作用域链恢复到原始状态

在严格模式下禁止使用with语句，非严格模式，不推荐使用with语句。使用with语句js非常难以优化，尽可能避免使用with语句

在对象嵌套层次很深的时候，通常使用with语句来简化代码编写。例如下面这个栗子：
```
document.forms[0].address.value
```
如果这样的代码多次出现，则可以使用with语句将form对象添加到作用域链顶层：
```
with(document.forms[0]){
  // 直接访问表单元素
  name.value = "";
  address.value = "";
  email.value = "";
}
```
这样就减少大量的输入，不用再为每个属性名添加documents.forms[0]前缀。这个对象临时挂载在作用域链上，
当js需要解析如address的标示符时，就会自动在这个对象中查找。当然不使用with的等价代码形式：
```
var f = document.forms[0];
f.name.value = '';
f.address.value = '';
f.email.value = '';
```

需要注意的是，只有查找标示符时，才会用到作用域链，创建新的变量时候，不使用它.

看看这段代码:
```
with(o) x=1;
```

如果对象o有一个属性x，那么这行代码给这个属性赋值为1。但是如果o中没有这个属性x，这段代码和不使用with的代码
`x = 1;`是一样的。它给一个或全局变量x赋值，或者创建全局变量的新属性x。

**简单来说，就是with提供来读取o属性的快捷方式，但是不能创建o的属性**

### debugger语句

程序员经常需要打一些断点来查看程序是否在按照自己设计正确运行，debugger语句就是让js解释器以调试模式
运行，来产生一个断点，js执行到断点位置，停止运行，这时可以使用调试器输出变量的值，检查程序调用栈等等。

在ECMAScript5中，debugger语句正式加入语言，并且已经得到主流浏览器厂商的支持。

debugger语句不会启动调试器，但如果调试器已经在运行，这条语句才会真正产生一个断点，例如在使用Chrome开发者工具
中的命令行时，debugger语句才会正常工作

### "use strict"
`"use strict"` 是ECMAScript5中引入的一条指令。

指令并不是语句，指令和语句有2个重要的区别：
- 语句不包含任何语言的关键字，指令仅仅包含一个特殊字符串直接量表达式，对于没有实现ECMAScript5的js解释器来说，只是一条没有副作用的表达式语句，什么都没执行
- 只能出现在脚本代码的开始或者函数体的开始、任何实体语句之前。在脚本或者函数体内第一条常规语句之后的字符串直接量表达式语句只当作普通的表达式语句对待，不会被当作指令解析

使用"use strict"指令的目的是说明，后续的代码将被解析成严格代码。

严格代码以严格模式执行。ECMAScript5的严格表达式是该语言的受限的子集，修正语言的重要缺陷，并且提供健壮的查错功能和增强的安全机制

严格模式和非严格模式区别如下:(前3条非常重要)
- 在严格模式中禁止使用with语句
- 所有的变量都需要先声明，如果给一个未声明的变量、函数、函数参数、catch从句参数或全局变量的对象赋值，将会抛出一个引用错误异常（非严格模式，这种隐式声明的全局变量的方法是给全局对象新添加一个新属性）
- 调用的函数（不是方法）中一个this值是undefined。（在非严格模式中，调用的函数中的this值总是全局对象。可以利用这种特性来判断js实现是否支持严格模式
> `var hasStrictMode = (function(){ "use strict"; return this===undefined;});`

- 在严格模式中，通过call()或apply()来调用函数时，其中的this值就是通过call()或apply()传入的第一个参数（非严格模式中，null和undefined值被全局对象和转换为对象的非对象值所代替）
- 在严格模式中，给只读属性赋值和给不可扩展的对象创建新成员都将抛出一个类型错误异常(非严格模式，这些操作只是简单的失败，不会报错)
- 在严格模式中，传入eval()的代码不能调用程序所在的上下文中声明变量或定义函数，而在非严格模式可以的。相反，变量和函数的定义是在eval()的新作用域中，这个作用域在eval()返回时就被弃用了
- 在严格模式中，函数的arguments对象拥有传入函数值的静态副本。而非严格模式，arguments对象具有魔术般行为，arguments里的数组和函数参数都是指向同一个值的引用
- 在严格模式中，当delete运算符后跟随非法的标示符时，将会抛出一个语法错误异常（非严格模式，这种delete表达式将什么都不会做，并返回false）
- 在严格模式中，试图删除一个不可配置的属性将抛出一个类型错误异常（非严格模式，这种delete表达式操作失败，并返回false）
- 在严格模式中，在一个对象直接量中定义两个或多个同名属性将产生一个语法错误（非严格模式中不会报错）
- 在严格模式中，函数声明中存在两个或多个同名参数将会产生一个语法错误（在非严格模式中不会报错）
- 在严格模式中，不允许使用八进制数直接量（以0为前缀，非严格模式中某些实现是允许八进制数直接量的）
- 在严格模式中，标示符eval和arguments当作关键字，他们的值是不能更改的。不能给这些标识符赋值，也不能把它们声明为变量、用作函数名、用作函数参数或者catch块的标识符
- 在严格模式中，限制了对调用栈的监测能力，arguments.caller和arguments.callee都会抛出一个类型错误异常。在严格模式的函数同样有caller和arguments属性，当访问这两个属性值都将抛出类型错误异常

## js语句总结表
| 语句       | 语法                                                         | 用途                                                                                      |
|:-----------|:-------------------------------------------------------------|:------------------------------------------------------------------------------------------|
| break      | break [label];                                               | 退出最内层循环或者退出switch语句，又或者退出label所指定的语句／switch语句中标记的一条语句 |
| case       | case expression:                                             | 在switch中标记一条语句                                                                    |
| continue   | continue [label];                                            | 重新开始最内层的循环或重新开始label指定的循环                                             |
| debugger   | debugger;                                                    | 断点起调试                                                                                |
| default    | default;                                                     | 在switch中标记默认的语句                                                                  |
| do/while   | do statement while(expression);                              | while循环的一种替代形式                                                                   |
| empty      | ;                                                            | 什么都不做                                                                                |
| for        | for(init;test;incr)statement                                 | 一种简写的循环                                                                            |
| for/in     | for(var in object) statement                                 | 遍历一个对象的属性                                                                        |
| function   | function name([para[],...]){body}                            | 声明一个函数                                                                              |
| if/else    | if(expr)statement1 [else statement2]                         | 执行statments1或者statements2                                                             |
| label      | label:statement                                              | 给statement指定一个名字                                                                   |
| return     | return [expression];                                         | 从函数返回值                                                                              |
| switch     | switch(expr){statements}                                     | 用case或者'default:'语句标记多分支语句                                                    |
| throw      | throw expression;                                            | 抛出异常                                                                                  |
| try        | try {statements} [catch {statements}] [finally {statements}] | 捕获异常                                                                                  |
| use strict | "use strict"                                                 | 对脚本和函数应用严格模式                                                                  |
| var        | var name = [expr][,...];                                     | 声明并初始化一个或多个变量                                                                |
| while      | while(expr) statements                                       | 基本的循环结构                                                                            |
| with       | with(object) statements                                      | 扩展作用域链                                                                              |
