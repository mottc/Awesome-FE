# 词法结构

- 字符集：unicode
- 区分大小写，关键字、变量、函数名、标示符必须采取大小写一致
- 注释  
  ```
  // 单行注释
  /* ~一段注释~ */ // 另一段注释
  /*
   * 多行注释
   * 多行注释
  */
  ```
- 直接量
  ```
  12  // 数字
  1.2 // 小数
  "hello world" // 一个字符串
  'hi'  // 另一种字符串
  true  // 布尔值
  /^javascript$/gi //正则表达式直接量
  null // 空
  {  x:1 ,y:2}  // 对象
  [ 1,2,3,4,5 ] //数组
  ```
- 标示符、保留字
  [](https://github.com/ZhaoLion/Awesome-FE/blob/master/JS/%E5%9F%BA%E7%A1%80/js%E4%BF%9D%E7%95%99%E5%85%B3%E9%94%AE%E5%AD%97%E5%8F%8A%E5%8D%B1%E9%99%A9%E5%8F%98%E9%87%8F%E5%90%8D.md)

- 可选的分号
  1. 在任何需要分割的地方使用 `;` 进行分隔
  2. 在任何可以省略分号的地方都将其省略   

  如果不使用分号，由于语句的分隔规则，会导致一些意想不到的情况，建议无论什么时候都使用分号进行分割

# 类型、值和变量
js中的数据类型：
  - 数字
  - 字符串
  - 布尔值
  - null
  - undefine
  - 对象

js数据类型分为2类：`原始类型` 和 `对象类型`
  > 原始类型：
  - 数字
  - 字符串
  - 布尔值
  - *特殊的原始值：‘null’ 和 ‘undefine’*

  > 对象类型：  
  - 属性的集合
  - 数组
  - 函数


  ## 变量声明
  js中通过`var`关键字来声明一个变量

  ```
  var a = 1;
  var a,b;
  var i=0,j=1,k=2;
  ```

  如果未在var语句中，就给变量指定初始值，那么虽然声明这个变量，但是给它存入一个值前，初始值是undefined

  **重复声明一个变量合法，且没有任何危害**

  ### 变量作用域

  全局变量拥有全局作用域

  函数内声明的变量和函数参数都是局部变量，只能在函数体内有定义

  函数体内，局部变量优先级高于全局变量，同名局部变量覆盖全局变量

  ```
  var scope = "global"; 
  function check() {
    var scope = "local";
    return scope; // 返回"local"
  }
  a = check(); // => "local"
  ```

  ### 声明提前
  js的函数作用域指的是，在函数内声明的所有变量，在函数体内始终可以看到，变量在声明之前甚至已经可以使用，这个特性称为“声明提前”

  看下下面一段代码，你可能会认为第一个打印"global",因为代码没有执行到var语句。其实，局部变量在函数体内始终有定义，也就是说，
  函数体内局部变量覆盖同名全局变量。但是只有执行到var语句时局部变量才会赋值，因此，上面的执行过程相当于，将函数变量声明
  “提前”函数体顶部，同时初始化位置仍然留在原来位置

  ```
  var scope = "global";
  function check() {
    console.log(scope);  // "undefined"
    var scope = "local"; // 赋初始值
    console.log(scope); // “local”
  }
  ```

  ### 作为属性的变量
  js的全局变量，其实是定义了全局对象的一个属性。    
  当使用var声明一个变量，创建的这个属性是不可以配置的。无法通过delete删除    
  如果给一个未声明的变量赋值，js会自动创建一个全局变量，是全局对象的正常可配置的属性，能够通过delete删除

  ```
  var some = 1;
  gvar = 1;
  delete some; // => false，变量没被删除
  delete gvar; // => true,变量被删除
  ```

## 数字
### 整型直接量
js不区分整数值和浮点数值，所有的数字均用浮点数值表示。js采用的时IEEE 754定义的64位浮点格式来表示数字，
然后需要注意，js中实际的操作（比如数组索引）则是基于32位整数的

支持的整型直接量
 -  十进制 1000
 -  十六进制 0x1F、0X39

部分ECMAScript实现是支持八进制的，但ECMAScript标准不支持八进制直接量，在ECMAScript6的严格模式下，八进制是明令禁止的

### 浮点型直接量
浮点型采用传统实数写法，可以采用指数计数法和更简洁的记法
- 3.14
- 7.03E-12
- .3333333

### 算术运算
运算符支持：`+`,`-`,`*`,`/`,`%`   

js还支持更为复杂的算术运算，通过作为Math对象的属性定义的函数和常量来实现   
```
Math.pow(2,53)  // 2的53次幂
Math.round(.6)  // => 1.0 四舍五入
Math.ceil(.6)   // => 1.0 向上求整
Math.floor(.6)  // => 0.0 向下求整
Math.abs(-4)    // 绝对值
Math.max(x,y,z) // 返回最大值
Math.min(x,y,z) // 返回最小值
Math.random()   // 生成一个0-1.0的随机数
Math.PI         // 圆周率
Math.E          // e，自然对数
Math.sqrt(3)    // 3的平方根
Math.sin(0)     // 三角函数
Math.log(10)    // 10的自然对数
Math.log(100)/Math.LN10   // 以10为底的对数
Math.log(512)/Math.LN2    // 以2为底的对数
Math.exp(3)     // e的3次幂
```

正无穷大：`Infinity`     
非数字值： `NaN`
```
Infinity                  // 将一个可读可写的变量初始化为Infinity
Number.POSITIVE_INFINITY  // Infinity，只读
1/0                       // Infinity
Number.MAX_VALUE + 1      // Infinity
Number.NEGTIVE_INFINITY   // 负无穷大
-Infinity                 // 负无穷大
-1/0                      // 负无穷大
-Number.MAX_VALUE - 1     // 将一个可读可写变量初始化为NaN
NaN                       // 非数字值
Number.NaN                // 非数字值，只读
0/0                       // NaN
Number.MIN_VALUE/2        // 下溢，计算结果为0
-Number.MIN_VALUE/2       // 负零
-1/Infinity               // 负零
-0                        // 负零，下溢，比js所能表示的0还小时，计算结果为0
```

负零和正零是相等的，除了作为除数之外
```
var zero = 0;
var negz = -0;
zero === negz;    // => true
1/zero === 1/negz // => false
```

### 二进制浮点数和四舍五入错误

js可以精确的表示分数，比如1/2、1/8,但不能精确表示0.1这样数字
```
var x = .3 - .2;
var y = .2 - .1;
x == y; // => false 两个值不相等
x == .1 // => false ,0.3 - 0.2 不等于 0.1
y == .1 // => true, 0.2 - 0.1 等于 0.1
```

### 日期和时间
js语言核心包括`Date()`构造函数，用来表示日期和时间
```
var then = new Date(2016.4.22); // 2016年4月22日
var later = new Date(2016,3,25,17,19,30) // 2016.4.25 17:19:30pm
var now = new Date(); // 当前时间和日期
var elapsed = now - then; // 日期减法，计算当前时间间隔的毫秒数
later.getFullYear(); //  => 2016
later.getMonth(); // => 3 ,月份从0开始
later.getDate() // => 25,从1开始的天数
later.getDay() // =>  1，星期几，0代表星期日，1代表星期1
later.getHours() // => 17 当地时间17:19pm
later.getUTCHours() // => 9 我所在UTC－8 使用UTC表示小时的时间，基于时区，所以返回9
```

### string (文本)
js是采用UTF－16编码的Unicode字符集，string是由一组16位值组成的 **不可变** 的有序序列，每个字符
通常来自于Unicode字符集。    
js通过字符串类型来表示文本。字符串的长度是其所含的16位值的个数。    
js字符串的索引从0开始，空字符串长度为0

js字符串直接量是由单引号或者双引号括起来的字符序列。
```
""
'test'
"3.14"
'name="myform"'
"Would't you prefer to say goobye?"
"this string\nhas two lines"
```

在ECMAScript3中，字符串直接量必须写在一行，而在ECMAScript5中，字符串直接量可以拆成数行，每一行
通过反斜线（`\`）结束，反斜线和行结束符都不算字符串直接量的内容
```
"two\nlines"

"one\
two\
three"

```

### 转义字符
在js中，反斜线有特殊用途，用来进行转义，不是原来的意思了

| 转义字符         | 含义                                       |
|:-----------------|:-------------------------------------------|
| \o               | NUL字符（\u0000）                          |
| \b               | 退格符（\u0008）                           |
| \t               | 水平制表符                                 |
| \n               | 换行符(\u000A)                             |
| \v               | 垂直制表符(\u000B)                         |
| \f               | 换页符(\u000C)                             |
| \r               | 回车符(\u000D)                             |
| \"               | 双引号(\u0022)                             |
| \'               | 单引号(\u0027)                             |
| \\               | 反斜线(\u005C)                             |
| \XXXXXXXX        | 两位16进制XXXXXXX指定的Latin－1字符        |
| \uXXXXXXXXXXXXXX | 4位十六进制XXXXXXXXXXXXXX指定的Unicode字符 |

### 字符串使用
jsn 内置功能之一就是字符串连接，将`+`用于字符串，则表示字符串连接
`msg = "Hello" + " " + "World"`

获取字符串长度: `s.length`

除了length属性，还提供许多调用方法：
```
var s = "hello,wolrd"
s.charAt(0)             // "h":第一个字符
s.charAt(s.length-1)    // "d":最后一个字符
s.substring(1,4)        // "ell": 第2-4个字符
s.slice(1,4)            // "ell": 第2-4个字符
s.slice(-3)             // "rld": 最后三个字符
s.indexOf("l")          // 2: l 首次出现的位置
s.lastIndexOf('l')      // 10: l最后出现的位置
s.indexOf('l',3)        // 3:  在位置3之后首次出现l的位置
s.split(",")            // ["hello","world"] 分割成字符串
s.replace('h','H')      // "Hello,world",将h替换成H
s.toUpperCase()         // "HELLO,WORLD",转成大写字符串
```

### 模式匹配
js定义了RegExp()函数，用来创建`文本匹配模式`的对象,称为正则表达式

RegExp不是js的基本数据类型，和Date一样，只是一种具有实用API的特殊对象，但是仍然具有直接量写法，
可以直接在js中使用，在两条斜线之间的文本构成正则表达式直接量。第二条斜线之后也可以跟随一个或多个字母，
用来修饰匹配模式含义

```
/^HTML/ //匹配以HTML开始的字符串
/[1-9][0-9]*/ // 匹配一个非零数字，后面是任意个数字
/\bjavascript\b/i // 匹配单词“javascript”，忽略大小写
```

RegExp对象定义有用的方法，字符串也有接收RegExp参数的方法

```
var text = 'testing: 1, 2, 3';  
var pattern = /\d+/g // 匹配所有包含一个或多个数字的实例
pattern.test(text)  // true 匹配成功
text.serch(pattern) // 9,首次匹配成功的位置
text.match(pattern) // ["1","2","3"] 所有匹配组成的数组
text.replace(pattern,"#") //"testing,#, #, #"
text.split(/\D+/) //["","1","2","3"] 用非数字截取字符串
```

## 布尔值
布尔值：`true`和`false`

比较语句结果通常是布尔值，`a==4`

任意js值都可以转换为布尔值，下面转换成false：
```
undefined
null
0
-0
NaN
"" // 空字符串
```
所有其他值，包括所有对象数组，都会转换成true

检测o是否是非null值,只有o不是null时才会执行if后面代码
`if( o !== null)...`

o不是任何假值才会执行if后面代码：
`if( o)...`

布尔值包含toString(),可以将字符串转换为`"true"`或`"false"`

布尔值运算符：`&&`(与)  、   `||`(或)   、   `！`(非)

## null和undefined
null: 描述"空值"
undefined: 未定义的值，表明变量没有初始化

尽管null和undefined不同，但是都表示值的空缺，往往可以互换
`null == undefined` // => true

null和undefined 都不包含任何属性和方法

## 全局对象
全局对象在js中有着重要用途，全局对象属性是全局定义的符号，js程序可以直接使用    
js解释器启动时，会创建一个的新的全局对象，并定义初始属性：

- 全局属性，比如undefined、Infinity和NaN
- 全局函数，比如isNaN(),parseInt()和eval()
- 构造函数，比如Date(),RegExp(),String(),Object()和Array()
- 全局对象，比如Math和JSON

全局对象的初始属性并不是保留字，但是应该当作保留字对待，还有Windows对象定义一些额外的全局属性，也应该保留

`var global = this; // 定义一个引用的全局对象的全局变量`

## 包装对象
js 对象是一种复合值，属性或已命名的集合。    
通过`.`符号来引用属性值
当属性值是一个方法时，称其为方法。通过O.m()来调用对象O中的方法

字符串同样具有属性和方法：
```
var s = "hello world!";
var word = s.substring(s.indexOf(' ')+1, s.length); // word="world!"
```

字符串既然不是对象，为啥有属性呢？   
因为引用了字符串s的属性，js会将字符串值通过调用`new String(s)`的方式转换成对象，这个对象继承了
字符串的方法，并被用来处理属性的引用。一但引用结束，这个新创建对象便被销毁了

同字符串一样，数字和布尔值也具有各自的方法：通过`Number()`和`Boolean`构造函数创建一个临时对象，
这些方法的调用均来自这个临时对象。   

null和undefined没有包装对象，访问他们的属性，会造成一个类型错误

看个栗子，思考一下执行结果：
```
var s = "test"; // 创建一个字符串
s.len = 4;      // 给s设置一个属性值，创建一个临时字符串对象，并且赋值len＝4，然后销毁这个临时对象
var t = s.len;  // 查询这个属性，通过原始的（没有修改过的）字符串值创建一个新的字符串对象，尝试读取len，属性不存在，t为undefined
```

存取字符串、数字、布尔值的属性时临时创建的对象叫做 **包装对象**

包装对象只是被看作一种实现细节，不需要特别关注。由于字符串、数字、和布尔值的属性都是只读的，
并且不能够定义新属性，与对象是有区别的

注意，可以通过`String()` `Number()` `Boolean()`构造函数显式创建包装对象：
```
var s = "test", n = 1, b = true;  // 一个字符串、数字、布尔值
var S = new String(s);  // 一个字符串对象
var N = new Number(n);  // 一个数字对象
var B = new Boolean(b); // 一个布尔值对象
```

js 会在必要时包装对象转换成原始值，因此上段代码中对象S、N、B常常，但不总是表现和值s、n、b一样。
`==`将原始值和其包装对象视为相等    
`===`将它们视为不相等,通过`typeof`运算符可以看到原始值和包装对象的不同

## 不可变的原始值和可变的对象引用
js 中原始值(`undefined`,`null`,`布尔值`,`数字`,`字符串`)与对象(包括数组和函数)有着根本区别。

- 原始值时不可更改的，任何方法都无法更改（或者`突变`）一个原始值
> 对数字和布尔值来说显然如此－改变数字值本身就说不通，对字符串来说不是很明显。
> 字符串是由字符组成数组，我们希望通过指定索引来修改字符串中的字符。实际上js禁止这样的行为，
> 字符串方法看上去返回修改后的字符串，实际上是返回新的字符串值
> 比如：
```
var s = "hello"; // 创建一个小写组成的字符串
s.toUpperCase(); // 返回"HELLO",但是没有改变s的值
s                // s＝“hello”，s原字符串并没有改变
```

- 原始值的比较只是值的比较
> 原始值只有在值相等时才相等，对于数字、布尔值、null和undefined来说比较容易理解，对于字符串则不明白了
> 单独比较2个字符串，只有2个字符串长度相等且每个索引的字符都相等，才是相等

- 对象是可变的，值是可修改的
> 栗子：  
```
var o = { x:1 }; // 定义一个对象
o.x = 2;         // 修改对象属性值来修改对象
0.y = 3;         // 再次修改对象，增加一个属性－y
var a = [1,2,3]  // 数组也是可修改的
a[0] = 0;        // 更改数组的一个元素
a[3] = 4;        // 给数组增加一个新元素
```

- 对象的比较不是值的比较，而是对象引用的比较
> 即使2个对象包含同样的属性和相同值，也不是相等的
> 各个索引元素完全相等的两个数组也不相等。
```
var o = { x:1 }, p = { x:1 } // 具有同样属性和值的两个对象
0 === p // false ,两个单独的对象永远不相等
var a = [], b =[]  // 两个单独的空数组
a === b // false 两个单独的数组永远不相等
```

通常讲，对象被称为`引用类型`，以便将js基本类型区分。对象值都是引用，对象的比较都是引用的比较
当且仅当他们引用同一个对象时，才会相等
```
var a = []; // 定义一个空的数组
var b = a; // 变量b引用a
b[0] = 1; // 通过b的引用修改a
a[0];  // 1,a的值也修改了
a === b; // true，a和b引用同一个数组，相等
```

如上所示，将对象或数组赋值给一个变量，仅仅是赋值的引用值：对象本身没有被复制一次

如果想得到一个对象或者数组的副本，必须显示复制对象每一个属性或数组每一个元素    

例如循环来完成数组复制：
```
var a = [1,2,3];
var b = [];
for(var i = 0; i < a.length; i++){
  b[i] = a[i];
}
```

同样的，如果想比较2个单独的对象或者数组，必须比较全部的属性或者元素    
比较2个数组的函数:  
```
function equalArrays(a,b){
  if ( a.lengh != b.length) return false;
  for(var i=0; i<a.length; i++ ){
    if(a[i] !== b[i]) return false;
  }
  return true;
}
```

## 类型转换
| 值              | 转换为字符串   | 数字    | 布尔值  | 对象                  |
|:----------------|:---------------|:--------|:--------|:----------------------|
| undefined       | "undefined"    | NaN     | false   | throws TypeError      |
| null            | "null"         | 0       | false   | throw TypeError       |
| true            | "true"         | 1       | XXXXXXX | new Boolean(true)     |
| false           | "false"        | 0       | XXXXXXX | new Boolean(false)    |
| ""（空字符串）  | XXXXXXX        | 0       | false   | new String("")        |
| "1.2"           | XXXXXXX        | 1.2     | true    | new String("1.2")     |
| "one"           | XXXXXXX        | NaN     | true    | new String("one")     |
| 0               | "0"            | XXXXXXX | false   | new Number(0)         |
| -0              | "0"            | XXXXXXX | false   | new Number(-0)        |
| NaN             | "NaN"          | XXXXXXX | false   | new Number(NaN)       |
| Infinity        | "Infinity"     | XXXXXXX | true    | new Number(Infinity)  |
| -Infinity       | "-Infinity"    | XXXXXXX | true    | new Number(-Infinity) |
| 1(无穷大，非零) | "1"            | XXXXXXX | true    | new Number(1)         |
| {}              | 复杂           | 复杂    | true    | XXXXXXX               |
| []              | ""             | 0       | true    | XXXXXXX               |
| [9]             | “9”            | 9       | true    | XXXXXXX               |
| ['a']           | 使用join()方法 | NaN     | true    | XXXXXXX               |
| function(){}    | 复杂           | NaN     | true    | XXXXXXX               |

原始值到对象的转换也很简单，原始值调用`String()`,`Number()`,`Boolean()`构造函数，转换为各自的包装对象

null 和 undefined属于例外，当做是一个对象的地方都会产生一个类型错误异常，不会进行正常类型转换

### 转换和相等性
js可以做灵活的类型转换，相等运算符也跟相等的含义一样，灵活多变    
下面的比较结果都是true:
```
null == undefined; // 这两个值被认为相等
"0" == 0;   // 比较之前，字符串转换成数字
0 == false; //  比较之前，布尔值转换成数字
"0" == false; // 比较之前字符串和布尔值都转换成数字
```

**需要注意，一个值转换成另一个值不代表两个值相等。**

如果在期望使用布尔值的地方使用undefined,会转换成false，但不代表undefined == false

js中，if语句将undefined转换成false，但 `== `运算符不会试图将操作数转换为布尔值

## 显示类型转换
为了使代码更加清晰明了，经常使用显示转换，最简单的方法就是不使用new运算符来调用Boolean()、Number()、
String()，Object()函数
```
Number("3") // '3'=>3
String(false) // false => "false"
Boolean([]) // => true
Object(3) // => new Number(3)
```

除了null和undefined以外都有toString方法，一般执行结果与String()返回结果一致  

如果试图把null 和 undefined 转换为对象，会抛出一个类型错误。如果使用object()则不会抛出异常，仅仅
简单的返回一个新创建的空对象

**js中某些运算符会做隐式的类型转换**
- `+`运算符
> 一个操作数是数字，另一个操作数是字符串，则会把非字符串的操作数转换成字符串然后拼接之后返回（非字符串操作数不会改变类型）
> `1+'1' // => '11'(String)`
> `x + '' // => 等价于String(x)`
- `!`运算符
> 会把操作数转换为布尔值并取反。（操作数不会改变类型）
> `!!x // 等价于Boolean(x)`

**Number => String**
- Number类定义的toString()方法可以接受表示转换基数的可选参数，如果不指定，则转换基于十进制
```
var n = 17;
binary_string = n.toString(2);
octal_string = "0" + n.toString(8);
hex_string = "0X" + n.toString(16);
```
- 控制小数点位置和有效数字位数
1. toFixed() 根据小数点后指定位数将数字转换为字符串，从不使用指数计数法
2. toExponential() 根据指数记数法将数字转换为指定形式字符串
3. toPrecision() 根据指定的有效位数将数字转换为字符串。如果有效数字的位数少于数字整数部分位数，转换成指数形式
```
var n = 123456.789;
n.toFixed(0); // '123457'
n.toFixed(2); // '123456.79'
n.toFixed(5); // '123456.78900'
n.toExponential(1); // '1.2e+5'
n.toExponential(3); // '1.235e+5'
n.toPrecision(4); // '1.235e+5'
n.toPrecision(7); // '123456.8'
n.toPrecision(10); // '123456.7890'
```

**String => Number**
- Number() 接受传入一个字符串，试图将其转换为一个整数或者浮点数直接量，基于十进制数转换，且不能带非法字符
- parseInt() 只解析整数，并且可以通过字符串前缀“0X”或"0x" 解析为16进制数
- parseFloat 解析浮点数和整数

```
parseInt("3 asd"); // => 3
parseInt("3.124"); // => 3
parseInt("0xff"); // => 255
parseInt("-0x7f"); // => -127

parseFloat("3.14 asdas") // => 3.14
parseFloat(".1") // => 0.1

parseInt(".1") // => NaN 整数不能以`.`开始
parseFloat("$111.11") // => NaN 数字不能以"$"开始
```

parseInt 可以接收第二个可选参数，指定数字转换的基数，合法范围 2～36

```
parseInt("11",2); // ＝> 3
parseInt("ff",16); // => 255
parseInt("zz",36); // => 1295
parseInt("077",8); // => 63
parseInt("077",10); // => 77
```

**对象转换为原始值**
- Object => Boolean
> 所有对象（包括数组和函数）都转换为true

- Object => String
> toString()
> valueOf()

- Object => Number
> valueOf()
> toString()

js的对象到字符串转换步骤:
- 如果对象有toString方法，则调用这个方法。如果返回一个原始值，则js将这个值转换为字符串，返回字符串结果
- 如果对象没有toString方法，或者这个方法不返回原始值，则调用valueOf方法。如果存在这个方法，则js
调用。如果返回时原始值，js将这个值转换为字符串，然后返回字符串结果
- 如果没有以上两个方法，或者以上2个方法返回的不是原始值，会抛出一个类型错误异常

js的对象到数字转换过程:     
js转换数字过程与字符串过程差不多，只是优先使用valueOf
- 如果对象有valueOf方法，则调用这个方法。如果返回一个原始值，则js将这个值转换为字符串，返回字符串结果
- 如果对象没有valueOf方法，或者这个方法不返回原始值，则调用toString方法。如果存在这个方法，则js
调用。如果返回时原始值，js将这个值转换为字符串，然后返回字符串结果
- 如果没有以上两个方法，或者以上2个方法返回的不是原始值，会抛出一个类型错误异常

**为什么空数组和单个数字数组会被转换成0和单个数字？**
- 数组继承了Object默认的valueOf方法，返回一个对象而不是原始值，因此调用toString()方法，这个方法返回一个原始值
因此数组到数字的转换为空字符串，空字符串转换成数字0
- 含有一个元素的数组转换成字符串结果和单个元素转换字符串的结果一样。转换成单个数字的字符串，然后转换成数字

**"＋"运算符的一个数字，一个操作数是对象，情况如何？**
js将使用“特殊方法”将对象转换成原始值，而不是其他运算符的方法执行对象到数字的转换，“==”运算符与此类似。
如果将对象和原始值比较，则转换会将对象到原始值的转换方式进行

**“＋”、“==”应用在对象到原始值的转换特殊情形**
如果涉及到日期对象，而日期类是js中唯一的预先定义类型，定义了有意义的向字符串和数字的转换。  
对于所有非日期对象，对象到原始值的转换基本上是对象到数字的转换，也就是首先调用valueOf。   
对于日期对象，则使用对象到字符串的转换模式，通过valueOf或toString返回的原始值被直接使用，而不会被强制转换为数字或字符串，与其他的转换有一些不同

**"<"运算符**
所有关系运算符对对象做对象到原始值的转换，但要出去日期对象情形。任何对象都好首先尝试调用valueOf，然后调用toString。
不管得到的原始值能否被直接使用，都不会进一步转换为数字或字符串。

**"+" "==" "!=" 和关系运算符是唯一执行这种特殊的字符串到原始值的转换方式的运算符**
其他运算符到特定类型的转换都很明确，而且对日期对象来讲，也没有特殊情形
```
var now = new Date();
typeof(now + 1); // "string","+"将日期转换为字符串
typeof(now - 1); // "number" ，"-" 将使用对象到数字的转换
now == now.toString(); // true ,隐式的和显式的字符串转换
now > (now - 1); // true，">"将日期转换为数字
```
