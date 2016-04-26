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

| 转义字符 | 含义                             |
|:---------|:---------------------------------|
| \o       | NUL字符（\u0000）                |
| \b       | 退格符（\u0008）                 |
| \t       | 水平制表符                       |
| \n       | 换行符(\u000A)                   |
| \v       | 垂直制表符(\u000B)               |
| \f       | 换页符(\u000C)                   |
| \r       | 回车符(\u000D)                   |
| \"       | 双引号(\u0022)                   |
| \'       | 单引号(\u0027)                   |
| \\       | 反斜线(\u005C)                   |
| \xXX     | 两位16进制XX指定的Latin－1字符   |
| \uXXXX   | 4位十六进制XXXX指定的Unicode字符 |

### 字符串使用
jsn 内置功能之一就是字符串连接，将`+`用于字符串，则表示字符串连接
`msg = "Hello" + " " + "World"`

获取字符串长度: `s.length`

除了length属性，还提供许多调用方法：
```
var s = "hello,wolrd"
s.charAt(0)             // "h":第一个字符
s.charAt(s.length-1)    // "d":最后一个字符
s.subString(1,4)        // "ell": 第2-4个字符
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
