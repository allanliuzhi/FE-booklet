# toString()方法

　　本文将介绍toString()方法，toString()方法返回反映这个对象的字符串

&nbsp;

【1】undefined和null没有toString()方法

<div class="cnblogs_code">
<pre>undefined.toString();//错误
null.toString();//错误</pre>
</div>

&nbsp;

【2】布尔型数据true和false返回对应的'true'和'false'

<div class="cnblogs_code">
<pre>true.toString();//'true'
false.toString();//'false'
Boolean.toString();//"function Boolean() { [native code] }"</pre>
</div>

&nbsp;

【3】字符串类型原值返回

<div class="cnblogs_code">
<pre>'1'.toString();//'1'
''.toString();//''
'abc'.toString();//'abc'
String.toString();//"function String() { [native code] }"</pre>
</div>

&nbsp;

【4】数值类型的情况较复杂

<div class="cnblogs_code">
<pre>Number.toString();//"function Number() { [native code] }"</pre>
</div>

　　1、正浮点数及NaN、Infinity、-Infinity加引号返回

<div class="cnblogs_code">
<pre>1.23.toString();//'1.23'
NaN.toString();//'NaN'
Infinity.toString();//'Infinity'
-Infinity.toString();//'-Infinity'</pre>
</div>

　　2、负浮点数或加'+'号的正浮点数直接跟上.toString()，toString()无效并返回原数值

<div class="cnblogs_code">
<pre>+1.23.toString();//1.23
typeof +1.23.toString();//'number'
-1.23.toString();//-1.23
typeof -1.23.toString();//'number'</pre>
</div>

　　3、整数直接跟上.toString()形式，会报错，提示无效标记，因为整数后的点会被识别为小数点

<div class="cnblogs_code">
<pre>0.toString();//Uncaught SyntaxError: Invalid or unexpected token</pre>
</div>

　　因此，为了避免以上无效及报错的情况，数字在使用toString()方法时，加括号可解决

<div class="cnblogs_code">
<pre>(0).toString();//'0'
(-0).toString();//'0'
(+1.2).toString();//'1.2'
(-1.2).toString();//'-1.2'
(NaN).toString();//'NaN'</pre>
</div>

　　此外，数字类型的toString()方法可以接收表示转换基数(radix)的可选参数，如果不指定此参数，转换规则将是基于十进制。同样，也可以将数字转换为其他进制数(范围在2-36)

<div class="cnblogs_code">
<pre>var n = 17;
n.toString();//'17'
n.toString(2);//'10001'
n.toString(8);//'21'
n.toString(10);//'17'
n.toString(12);//'15'
n.toString(16);//'11'</pre>
</div>

&nbsp;

【5】对象Object类型及自定义对象类型加括号返回[object Object]

<div class="cnblogs_code">
<pre>{}.toString();//报错，Unexpected token .
({}).toString();//[object Object]
({a:123}).toString();//[object Object]
Object.toString();//"function Object() { [native code] }"</pre>
</div>
<div class="cnblogs_code">
<pre>function Person(){
    this.name = 'test';
}
var person1 = new Person();
person1.toString();//"[object Object]"</pre>
</div>

**类型识别**

 　　常常使用Object.prototype.toString()来进行类型识别，返回代表该对象的[object 数据类型]字符串表示

　　[注意]Object.prototype.toString()可以识别标准类型及内置对象类型，但不能识别自定义类型

<div class="cnblogs_code">
<pre>console.log(Object.prototype.toString.call("jerry"));//[object String]
console.log(Object.prototype.toString.call(12));//[object Number]
console.log(Object.prototype.toString.call(true));//[object Boolean]
console.log(Object.prototype.toString.call(undefined));//[object Undefined]
console.log(Object.prototype.toString.call(null));//[object Null]
console.log(Object.prototype.toString.call({name: "jerry"}));//[object Object]

console.log(Object.prototype.toString.call(function(){}));//[object Function]
console.log(Object.prototype.toString.call([]));//[object Array]
console.log(Object.prototype.toString.call(new Date));//[object Date]
console.log(Object.prototype.toString.call(/\d/));//[object RegExp]
function Person(){};
console.log(Object.prototype.toString.call(new Person));//[object Object]</pre>
</div>
<div class="cnblogs_code">
<pre>function type(obj){
    return Object.prototype.toString.call(obj).slice(8,-1).toLowerCase();
}
console.log(type("jerry"));//"string"
console.log(type(12));//"number"
console.log(type(true));//"boolean"
console.log(type(undefined));//"undefined"
console.log(type(null));//"null"
console.log(type({name: "jerry"}));//"object"

console.log(type(function(){}));//"function"
console.log(type([]));//"array"
console.log(type(new Date));//"date"
console.log(type(/\d/));//"regexp"
function Person(){};
console.log(type(new Person));//"object"</pre>
</div>

**其他识别**

　　除了类型识别之外，还可以进行其他识别，如识别arguments或DOM元素

<div class="cnblogs_code">
<pre>(function(){
    console.log(Object.prototype.toString.call(arguments));//[object Arguments]
})()
console.log(Object.prototype.toString.call(document));//[object HTMLDocument]</pre>
</div>

&nbsp;

【6】函数Function类型返回函数代码

　　当我们对一个自定义函数调用toString()方法时，可以得到该函数的源代码；如果对内置函数使用toString()方法时，会得到一个'[native code]'字符串。因此，可以使用toString()方法来区分自定义函数和内置函数

<div class="cnblogs_code">
<pre>function test(){
    alert(1);//test
}
test.toString();/*"function test(){
                    alert(1);//test
                  }"*/
Function.toString();//"function Function() { [native code] }"</pre>
</div>

&nbsp;

【7】数组Array类型返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串

<div class="cnblogs_code">
<pre>[].toString();//''
[1].toString();//'1'
[1,2,3,4].toString();//'1,2,3,4'
Array.toString();//"function Array() { [native code] }"</pre>
</div>

&nbsp;

【8】时间Date类型返回表示当前时区的时间的字符串表示

<div class="cnblogs_code">
<pre>(new Date()).toString();//"Sun Jun 05 2016 10:04:53 GMT+0800 (中国标准时间)"
Date.toString();//"function Date() { [native code] }"</pre>
</div>

&nbsp;

【9】正则表达式RegExp类型返回正则表达式字面量的字符串表示

<div class="cnblogs_code">
<pre>/ab/i.toString();//'/ab/i'
/mom( and dad( and baby)?)?/gi.toString();//'mom( and dad( and baby)?)?/gi'
RegExp.toString();//"function RegExp() { [native code] }"</pre>
</div>

&nbsp;

【10】错误Error类型

<div class="cnblogs_code">
<pre>Error.toString();//"function Error() { [native code] }"
RangeError.toString();//"function RangeError() { [native code] }"
ReferenceError.toString();//"function ReferenceError() { [native code] }"
SyntaxError.toString();//"function SyntaxError() { [native code] }"
TypeError.toString();//"function TypeError() { [native code] }"
URIError.toString();//"function URIError() { [native code] }"</pre>
</div>

