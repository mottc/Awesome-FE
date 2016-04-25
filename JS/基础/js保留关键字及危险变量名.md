Javascript 的保留关键字（标识符）不可以用作变量、标签或者函数名。

有些保留关键字是作为 Javascript 以后扩展使用。

关键字是严格不允许，而浏览器定义的变量名或者类名在使用的时候注意确保作用域

# EMCAScript 中的关键字

| break    | case      | catch      | continue  | s            |
|:---------|:----------|:-----------|:----------|:-------------|
| abstract | arguments | boolean    | break     | byte         |
| case     | catch     | char       | class*    | const        |
| continue | debugger  | default    | delete    | do           |
| double   | else      | enum*      | eval      | export*      |
| extends* | false     | final      | finally   | float        |
| for      | function  | goto       | if        | implements   |
| import*  | in        | instanceof | int       | interface    |
| let      | long      | native     | new       | null         |
| package  | private   | protected  | public    | return       |
| short    | static    | super*     | switch    | synchronized |
| this     | throw     | throws     | transient | true         |
| try      | typeof    | var        | void      | volatile     |
| while    | with      | yield      |           |              |

**'*' 标记的关键字是 ECMAScript5 中新添加的。**

# JavaScript 对象、属性和方法

您也应该避免使用 JavaScript 内置的对象、属性和方法的名称作为 Javascript 的变量或函数名：

| abstract  | arguments | boolean  | break         | byte           |
|:----------|:----------|:---------|:--------------|:---------------|
| Array     | Date      | eval     | function      | hasOwnProperty |
| Infinity  | isFinite  | isNaN    | isPrototypeOf | length         |
| Math      | NaN       | name     | Number        | Object         |
| prototype | String    | toString | undefined     | valueOf        |

# Java 保留关键字

JavaScript 经常与 Java 一起使用。您应该避免使用一些 Java 对象和属性作为 JavaScript 标识符：

| 保留关键字 | －   | －        | －        | -| -                   |
|:-----------|:-----|:----------|:----------|:-----------------------|
| getClass   | java | JavaArray | javaClass | JavaObject	|JavaPackage |

# Windows 保留关键字

JavaScript 可以在 HTML 外部使用。它可在许多其他应用程序中作为编程语言使用。
在 HTML 中，您必须（为了可移植性，您也应该这么做）避免使用 HTML 和 Windows 对象和属性的名称
作为 Javascript 的变量及函数名：

| 保留关键字     | －                 | －                 | －            | -                  |
|:---------------|:-------------------|:-------------------|:--------------|:-------------------|
| alert          | all                | anchor             | anchors       | area               |
| assign         | blur               | button             | checkbox      | clearInterval      |
| clearTimeout   | clientInformation  | close              | closed        | confirm            |
| constructor    | crypto	decodeURI    | decodeURIComponent | defaultStatus |                    |
| document       | element            | elements           | embed         | embeds             |
| encodeURI      | encodeURIComponent | escape             | event         | fileUpload         |
| focus          | form               | forms              | frame         | innerHeight        |
| innerWidth     | layer              | layers             | link          | location           |
| mimeTypes      | navigate           | navigator          | frames        | frameRate          |
| hidden         | history            | image              | images        | offscreenBuffering |
| open           | opener             | option             | outerHeight   | outerWidth         |
| packages       | pageXOffset        | pageYOffset        | parent        | parseFloat         |
| parseInt       | password           | pkcs11             | plugin        | prompt             |
| propertyIsEnum | radio              | reset              | screenX       | screenY            |
| scroll         | secure             | select             | self          | setInterval        |
| setTimeout     | status             | submit             | taint         | text               |
| textarea       | top                | unescape           | untaint       | window             |

# HTML 事件句柄
除此之外，您还应该避免使用 HTML 事件句柄的名称作为 Javascript 的变量及函数名。

| 保留关键字 | －         | －          | －          |
|:-----------|:-----------|:------------|:------------|
| onblur     | onclick    | onerror     | onfocus     |
| onkeydown  | onkeypress | onkeyup     | onmouseover |
| onload     | onmouseup  | onmousedown | onsubmit    |
