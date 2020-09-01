---
layout: post
title: "[JAVASCRIPT] JavaScript Tutorial"
date: 2020-08-26 00:00:00
categories: [STUDY]
tags: [JAVASCRIPT]
last_modified_at: 2020-08-31
---

From [w3schools](https://www.w3schools.com/js/default.asp)
<br>With JavaScript

---

> WEB : HTML(내용) & JavaScript(동작) & CSS(레이아웃)

__JavaScript__

<p> : 정적인 html 위에서 동작하여 User와 상호작용함 = 동적.
<br>* html에서 js는 웹브라우저에 의해 실행.
</p>

---

__JavaScript Where To__

```{.html}
<!--Internal JavaScript-->
<script> function myFunction(){ ... }</script>

<!--External JavaScript-->
<script src = "/js/myScript.js" ></script>
```

<p>script는 body의 아래 부분에 선언하는 것이 빠름.</p>

---

__JavaScript Output__

```{.html}
<!--inner HTML-->
<script>
document.getElementById("demo").innerHTML = 5 + 6;
</script>

<!--for testing : html이 load된 다음에, 이를 실행하면 html이 없어지고 출력됨.-->
<script>
document.write(5 + 6);
</script>

<!--window : window 없이도 사용가능.-->
<script>
window.alert(5 + 6);
</script>

<!--console : F12눌러 Console창에서 확인 가능.-->
<script>
console.log(5 + 6);
</script>

<!--window print : 해당 화면 프린트.-->
<button onclick="window.print()">Print this page</button>
```

---

__JavaScript Variables__
```{.html}
<!--Comments-->
<script>
//single line comments
/*block comments*/
  </script>

<!--String-->
<script>
var x = 2 + 3 + "4"; //54
var y = "5" + 5 + 5; //555
</script>

* var : undefined

```

<p>#Variable
<br>* 변수이름은 _, $, 문자로 시작 가능.
<br>* 대소문자 구분.
</p>

---

__JavaScript Operators__

|divide|/|부동소수점으로 출력|
|exponentiation|**, Math.pow(x,y)|
|equalValue and equalType|===|
|!equalValue or !equalType|!==|
|ternary operator(3항)|?|

|typeof|return type of var|
|instanceof|return true, if it is instance of object type|

---

__JavaScript DataTypes__

```{.html}
<script>
//Numbers
var x = 16;
var y = 16.00;
var z = 123e5;

//Booleans
(x == y) //return true
(y == z) //return false

//String
var num = '3';
var name = "bok";

//Arrays(Object)
var arr = ["num", 2, 3]

//Objects
var obj = {num : 3, name : "bok"};

//undifined
var a;
var b = "";
b = undefined;

//Null
typeof undefined //undefined
typeof null //object

null === undefined //false
null == undefined //true

</script>
```

<p>primitive datatype</p>

|string|number|boolean|undefined|

<p>complex datatype</p>

|function|object(obj, arr, null)|

---

__JavaScript Functions__

```{.html}
<script>

function myFuncton(p1, p2){
return p1* p2;
}

document.getElementById("id").innerHTML = myFunction(1,2); //2
document.getElementById("id").innerHTML = muFunction; //print function define
</script>

```

---

__JavaScript Objects__

```{.html}
<script>
ver obj = {
  num : 3,
  name : "bok",
  id : function(){
    return this.num + ":" + this.name;
  }
};

var num = obj.num;
var name = obj["name"];
var id = obj.id();

</script>
```

---

__JavaScript Events__

```{.html}
<button onclick = "displayDate()">Date</button>

<script>
fuction displayDate(){
  document.getElementById("id").innerHTML = Date();
}
</script>

<p id = "id"></p>
```

|onchange|HTML 요소 변경|
|onclick|HTML 요소 클릭|
|onmouseover|HTML 요소 위에 마우스|
|onmouseout|HTML 요소에서 마우스를 멀리 이동|
|onkeydown|키보드 누를 때|
|onload|브라우저가 페이지 로딩을 완료했을 때|

[>HTML Events<](https://www.w3schools.com/jsref/dom_obj_event.asp)

---

__JavaScript String__

```{.html}
<script>
var s = "string" //type : string
var x = new String("string"); //type : object 그러나 속도가 느림.
var y = new String("string")

//obj vs string
(s == x) //true
(s === x) //false

//obj vs obj, cannot compare
(x == y) //false
(x === y) //false
</script>
```

<p>String Method</p>

```{.html}
<script>
var str = "aBcD and aBcD";

str.length; //13
str.indexOf("aBcD", 4); //9
str.lastIndexOf("aBcD"); //9

//(start, end)
str.slice(-4, 0) //"aBcD"
str.substring(4, 6) //"a"

//(start, len)
str.substr(-8, 3) //"and"

str.replace("aBcD", "ABCD") //"ABCD and aBcD"
//replace() -regular expession
str.replace(/ABCD/i, "1234"); //대소문자 구분 X
str.replace(/aBcD/g, "1234"); //전부 변환

str.toUpperCase() //"ABCD AND ABCD"
str.toLowerCase() //"abcd and abcd"

//concat()
var text = "A" + " " + "BC";
var text = "A".concat(" ", "BC");

str.trim()

str.charAt(pos)
s[pos] //s[0] = "s", doesnt work
s.split("") //[a,B,c,D, ,a,n,d, ,a,B,c,D]

</script>
```

<p> * String = immutable, replace는 가능하지만 수정은 불가
<br>* escape문자는 js에서는 유효. HTML에서는 유효</p>

---

__JavaScript Numbers__

```{.html}
<script>
//부동소수점의 부정확성
var x = 0.2 + 0.1; //0.30000000000000004
var x = (0.2 * 10 + 0.1 * 10) / 10;//0.3

//Numeric String의 연산
var x = "100";
var y = "10";

var z = x + y; //10010
var z = x - y; //90
var z = x * y; //1000
var z = x / y; //10

</script>
```

<p>Number Method</p>

```{.html}
<script>
var x = 9.656;
x.toString() //"9.656"

x.toExponential() //"9.656e+0"
x.toExponential(2) //"9.66e+0"
x.toExponential(6) //"9.656000e+0"

//소수점 자리수
x.toFixed() //"10"
x.toFixed(2) //"9.66"
x.toFixed(6) //"9.656000"

//length
x.toPrecision() //"9.7"
x.toPrecision(2) //"9.7"
x.toPrecision(6) //"9.65600"

</script>
```
<p>
* NaN -Not a Number : type = number
<br>* Infinity : type = number
<br>* x.valueOf() : Object에서 primitive로 변환
</p>

<p>Global JavaScript Methods about Number</p>

```{.html}
<script>
//Number()
Number(true) //1
Number("   10") //10
Number("10.2") //10.2
Number("10 hello") //NaN

//parseInt()
parseInt(true) //NaN
parseInt("10 20 30"); //10
parseInt("10.33") //10
parseInt("10 hello") //10
parseInt("hello 10") //NaN

//parseFloat()
parseFloat("10") //10
parseFloat("10.2 20.2 30.2"); //10.2
</script>
```

---

__JavaScript Arrays__

```{.html}
<script>
//print
var arr = [3, "bok", 30];
document.getElementById("id").innerHTML = arr; //3,bok,30

//iterate
var arr = ["a", "b", "c"];
var arrlen = arr.length;
var text = "<ul>";

//1. loop
for(i=0; i<arrlen; i++)
    text += ("<li>" + arr[i] + "</li>")

//2. forEach
function func(value){
    text += ("<li>" + value + "</li>")
}
arr.forEach(func);

text += "</ul>";

//Add element
var arr = ["a", "b", "c"];
arr.push("d");
arr[arr.length] = "e";
arr[10] = "f"; //공란 = undefine

//recognize array
typeof arr //object
Array.isArray(arr) //true
arr instanceof Array //true
</script>
```

<p>여러가지 이유로 배열을 선언할 때, new Array()보다 []를 써야함.</p>

---

__JavaScript Array Methods__

```{.html}
<script>
var alpha = ["a","b","c"];
document.getElementById("id").innerHTML = alpha.toString() //a,b,c
documnet.getElementById("id").innerHTML = alpha.join(" * ") //a * b * c

alpha.push("d"); //4
alpha.pop(); //d

//앞에서 push and pop
alpha.shift(); //a
alpha.unshift("a"); //3

//splice(추가할 위치의 인덱스, 제거할 요소의 수, 추가할 요소)
alpha.splice(1,1,"A","B"); //["a","A","B","c"]
alpha.splice(1,2); //["a","c"]

//return new array
alpha = alpha.concat(alpha, alpha); //["a","c","a","c","a","c"]
alpha.slice(3,6); //["c","a","c"]
</script>
```

---

__JavaScript Sorting Arrays__

```{.html}
<script>
//string sort
alpha = ["a","b","c"];
alpha.reverse(); //["c","b","a"]
alpha.sort(); //["a","b","c"]

//Numeric sort
var num = [1,11,3,23,5];
num.sort(); //[1,11,23,3,5] 문자열같이 dic으로 출력
num.sort( function(a, b){ return a-b} ); //[1,3,5,11,23]
num.sort( function(a, b){ return 0.5 - Math.random()} );

Math.max.apply(null, num); //==Math.max(1,11,3,23,5)
Math.min.apply(null, num);

//Object sort
var stu = [{num:1, name:"a"}, {num:2, name:"b"}, {num:3, name:"c"}]
    //number
stu.sort( function(a, b){ return a.num - b.num });
    //string
stu.sort(
    function(a, b){
        var x = a.name.toLowerCase();
        var y = b.name.toLowerCase();
        if(x < y) return -1;
        else if(x > y) return 1;
        return 0;
     });
</script>
```

---

__JavaScript Array Iteration__

```{.html}
<script>
var num = [1,2,3];

//Array.forEach() : 함수가 value, index, array를 순서로 인자라고 파악
var txt = "";
num.forEach(myfunc); //1/2/3
function myfunc(value, index, array){
    txt = txt + value + "/";
}

//Array.map() : return newarr, values가 없는 배열요소에 대해서는 실행X
var newnum = num.map(myfunc); //1,4,9
function myfunc(value, index, array){
    return value * 2;
}

//Array.filter() : return newarr
var newnum = num.filter(myfunc); //2,3
function myfunc(value, index, array){
    return value > 1;
}

//Array.reduce() : 단일값 생성, 왼쪽에서 오른쪽으로
var sum = num.reduce(myFunc); //7
function myFunc(total, value, index, array) {
  return total + value;
}

//Array.reduceRight() : 단일값 생성, 오른쪽에서 왼쪽으로
var sum = num.reduce(myFunc, 100); //107
function myFunc(total, value, index, array) {
  return total + value;
}

//Array.every() : 모든 요소가 테스트를 통과하는지 확인
var allOver0 = num.every(myFunc); //true
function myFunc(value, index, array) {
  return value > 0;
}

//Array.some() : 일부 요소가 테스트를 통과하는지 확인
var someOver1 = num.some(myFunc); //true
function myFunc(value, index, array) {
  return value > 1;
}

//Array.find() : 테스트를 통과하는 첫 요소 반환
var first = num.find(myfunc); //2
function myfunc(value, index, array) {
  return value > 1;
}

//Array.findIndex() : 테스트를 통과하는 첫 요소의 인덱스 반환
var first = num.findIndex(myfunc); //1
function myfunc(value, index, array) {
  return value > 1;
}
</script>
```

---

__JavaScript Random__

```{.html}
<script>
Math.random() //0~1
Math.floor(Math.random() * 10) + 1; //1~10
</script>
```

---

__JavaScript Booleans__

```{.html}
<script>
var x;
var x = 0;
var x = "";
var x = null;
var x = false;
var x = 10/"H"; //NaN

Boolean(x) //return false
</script>
```

---

__JavaScript Comparisons__

```{.html}
<script>
2 < 12 //true
2 < "12" //true
2 < "H" //false
"2" < "12" //false
"2" > "12" //true
</script>
```

---

__JavaScript Switch__

```{.html}
<script>
//JS에서 switch case는 === 으로 비교함.
var x = 0;
switch(x) {
    case 0:
        text = "number";
        break;
    case "0":
        text = "string";
        break;
    default :
        text = "No value";
}
</script>
```

---

__JavaScript For Loop__

```{.html}
<script>
//for in : 객체의 속성을 반복.

var stu = {num:1, name:"bok", age:20};
ver txt = "";
var x;
for(x in stu)
    txt += ( stu[x] + "*" ) // 1*bok*20*

//for of : 반복가능한 데이터 구조를 반복.

var num = [1,2,3];
ver txt = "";
var x;
for(x of alpha)
    txt += ( x + "*" ) // 1*2*3*

var str = "apple";
ver txt = "";
var x;
for(x of str)
    txt += ( x + "*" ) // a*p*p*l*e*

</script>
```

---

__JavaScript Labels__

```{.html}
<script>
//label : 특정 위치를 지정해 break와 continue문을 함께 사용가능.

var txt = "";

firstloop :
for(var i = 1; i < 5; i++){
    secondloop :
    for(var j = 1; j < 5;j++){
        if(j > 4) break; //가장 가까운 루프를 빠져나감.
        if(i == 2) break secondloop; //안쪽 루프를 빠져나감.
        if(i == 3) break firstloop; //바깥쪽 루프를 빠져나감.
        txt += ("(" + i + "," + j +")");
    }
//(1,1)(1,2)(1,3)(1,4)
}

</script>
```

---

__JavaScript Type Conversion__

* can Contain Value

|string|number|boolean|object|function|

* Can't Contain Value

|null|undefined|

* Object

|Object|Date|Array|String|Number|Boolean|

* Conversion

|Original Value|To Num|To Str|Tp Boolean|
|---|---|---|---|
|0|0|"0"|false|
|"0"|0|"0"|true|
|""|0|""|false|
|{}|NaN|"[object Object]"|true|
|[]|0|""|true|
|[20]|20|"20"|true|
|[10,20]|NaN|"10,20"|true|
|null|0|"null"|false|
|undefined|NaN|"undefined"|false|

---

__JavaScript Regular Expression__

```{.html}
<script>
//Regular Expression : Search Pattern을 형성하는 일련의 문자.
//Search Pattern은 주로 String method 중 search()와 replace()에 사용.
//ex)
    var str = "Visit W3Schools";
    var n = str.search(/w3schools/i);
</script>
```
* Regular Expression Modifiers

|i|대소문자 구분 X|
|g|모두 수행|
|m|multi line을 수행|

```{.html}
<script>
var str = "576500%!";
var patt1 = /[0-5]/g;
var result = str.match(patt1);// 5,5,0,0

var patt1 = /\d/g;
var result = str.match(patt1); //5,7,6,5,0,0

var patt1 = /50+/g;
var result = str.match(patt1); //500
</script>
```

* Regular Expression Patterns
1. Brackets

|[abc]|대괄호 안의 char이 있는 지 확인|
|[0-5]|대괄호 안의 num이 있는 지 확인|
|(x|y)|괄호 안의 값이 있는 지 확인|

2. Metacharacter

|\d|digit을 찾음|
|\s|공백을 찾음|
|\b|\bword,일때는 word로 시작하는 부분이 있는지, word\b일때는 word로 끝나는 부분이 있는지 확인|

3. Quantifiers

|n+|n이 1개 이상 있는지 확인|
|n*|n이 0개 이상 있는지 확인|
|n?|n이 0개 또는 1개 있는지 확인|

* RegExp Object

```{.html}
<script>
//test() : 문자열에서 패턴을 검색하고 true/false를 반환
/e/.test("The best things in life are free!"); //문자열에 e가 있으므로 true

//exec() : 문자열에서 패턴을 검색하고 찾은 텍스트를 객체로 반환
var obj = /e/.exec("The best things"); //
obj[0] //e
obj.index //2
obj.input //The best things

</script>
```

---

__JavaScript Err__

```{.html}
<script>
//RangeError : 유효한 값 범위를 벗어난 숫자를 사용
var num = 1;
num.toPrecision(200);

//ReferenceError : 선언되지 않은 변수를 참조
var x;
x = y + 1;

//SystaxError : 문법 오류가 있는 코드를 평가할 때
eval("alert('Hello)");

//TypeError : 예상 유형의 범위를 벗어난 값 사용
var x = 1;
x.toUpperCase();
</script>
```

---

__JavaScript Hoisting__

```{.html}
<script>
//Hoisting : 모든 선언을 현재 범위의 맨 위로 이동하는 동작, var만 가능
//아래코드 둘은 같은 결과를 가지고 옴.
x = 5;
var x;

var x;
x = 5;

//선언만 가지고옴(아래 코드 둘을 같은 결과를 가지고옴.)
var x = 5;
var y;
document.getElementById("id").innerHTML = "x:" + x + ",y:" + y; //x:5,y:undefined
y = 7;
</script>
```

---

__JavaScript Strict__

["use strict"](https://www.w3schools.com/js/js_strict.asp)

---

__JavaScript Let__

```{.html}
<script>
//{} : Block Scope, 내부에 선언된 변수는 외부에서 접근할 수 없음.
//동일한 범위 또는 블록에서 let을 다시 선언하는 것은 불가함.

var x = 10;
{
let x = 2;
}
document.getElementById("id").innerHTML = x; //10

let i = 5;
for (let i = 0; i < 10; i++) {
}
document.getElementById("id").innerHTML = i; //5
</script>
```

---

__JavaScript Const__

```{.html}
<script>
//const는 선언과 초기화가 동시에 이루어짐.
//primitive 값은 변경불가
const x = 10;
x = 20; //error

//object는 변경 가능
const stu = {num:1,name:"bok"};
stu.num = 3;

//const array도 요소 변경가능.
const arr = ["a","b","c"];
arr[0] = "s";
arr.push("p");

//그래도 동일한 범위나 블록에서 존재하는 const에 재할당은 불가.
stu = {num:2,name:"lee"}; //error
arr = ["a","n"]; //error

</script>
```

---

__JavaScript Arrow__

```{.html}
<script>
hello = () => "Hello World!";
hello = (val) => "Hello" + val;

//this의 차이
<button id="btn">Click Me!</button>
document.getElementById("btn").addEventListener("click", hello);

//Regular Function : 호출하는 객체
hello = function() {
  document.getElementById("demo").innerHTML += this; //[object HTMLButtonElement]
}
//Arrow Function : this 기능의 소유자
hello = () => {
  document.getElementById("demo").innerHTML += this; //[object Window]
}

</script>
```

---

__JavaScript Debugging__

```{.html}
<script>
//console.log()
var a = 4;
var b = 5;
var c = a + b;
console.log(c);

//debugger : keyword로 F12를 통해서 가능
var x = 15 * 5;
debugger;
</script>
```

|F8|코드 계속 실행|
|F10|다음 함수로 이동|
|F11|함수의 내부 코드 이동|
|F11+shift|현재 함수에서 빠져나와 다음 함수로|

---

__JavaScript Style Guide__

<p>
* 변수 이름 : CamelCase
<br>* 연산자 주변에 공백
<br>* 코드 들여쓰기(tap말고 두개의 공백)
<br>* 세미콜론;
<br>* 가독성을 위해, 코드 길이는 한줄에 80이하(연산자 뒤, 쉼표 뒤)
<br>* 가능하면 소문자로 파일이름 작성.
<br>* 전역변수, new, ==, eval()을 피하기.
<br>* 선언은 상단에.(hoisting)
<br>* 변수 선언시 초기화.(object보다는 primitive으로)
</p>

```{.html}
var x1 = {};           // new object
var x2 = "";           // new primitive string
var x3 = 0;            // new primitive number
var x4 = false;        // new primitive boolean
var x5 = [];           // new array object
var x6 = /()/;         // new regexp object
var x7 = function(){}; // new function object
```

---

__JavaScript Mistakes__
<p>
* 덧셈연결
<br>* 부동소수점 계산(정확성을 위해, 곱하여 정수로 만들고 계산후 나누어야함.)
<br>* switch문에서 === 이용함.
<br>* 문자열 중간에 분리하기.(\사용)
<br>* null과 undefined는 다름.
</p>

```{.html}
if (typeof myObj !== "undefined" && myObj !== null)
```

---

__JavaScript Performance__

<p>* HTML에 접근할 때, 시간이 느리므로, 한번 접근하고 지역변수로 사용.</p>

```{.html}
var obj;
obj = document.getElementById("id");
obj.innerHTML = "HI";
```

<p>* 불필요한 변수 만들지 않기</p>

```{.html}
document.getElementById("demo").innerHTML = firstName + " " + lastName;
```

<p>* 페이지 하단에 스크립트를 배치하면, 브라우저가 페이지를 먼저 로드할 수 있음.</p>

```{.html}
window.onload = function() {
  var element = document.createElement("script");
  element.src = "myScript.js";
  document.body.appendChild(element);
};
```

<br>
<br>



