---
title: JavaScript - Scope & Hoisting
category: JavaScript
date: 2016-05-25 22:01:39
tags: JavaScript
---

## Variable Scope

* Scope(作用域)是指你的程式碼中該變數定義的區域(region)。
* 全域變數(global variable)定義在函式作用域之外，或者沒宣告就直接使用的變數。
* 區域變數(local variable)，指在函式中宣告的變數或函式參數，在函式外無法存取。

<!--more-->
### 1. 在函式主體中，區域變數的優先性(precedence)比同樣名稱的全域變數高。如果你宣告了一個區域變數或函式參數，其名稱與某個全域變數相同，你等於隱藏了那個全域變數


{% codeblock lang:js %}
var scope = "global";    // 宣告全域變數
function checkscope() {
  var scope = "local";   // 宣告區域變數
  return scope;          // Return 區域變數
}
checkscope()             // => "local"
{% endcodeblock %}

### 2. 雖然在全域Scope中，宣告變數可以不使用var。但一定要用var宣告區域變數
{% codeblock lang:js %}
scope = "global";          // 宣告全域變數 scope
function checkscope2() {
  scope = "local";         // 對全域變數 scope 做了變更
  myscope = "local";       // 宣告一個新的全域變數 myscope
  return [scope, myscope]; // Return two values.
}
checkscope2()              // => ["local", "local"]: 有副作用(side effects)
scope                      // => "local": 全域變數被改變了
myscope                    
{% endcodeblock %}

## Function Scope and Hoisting

* Function Scope 是指所有在函式內宣告的變數，在整個函式主體中都可見。這也表示變數甚至在它們被宣告前就是可見的，我們稱為hoisting(提升)。
* hoisting: 程式碼會表現的好像函式中所有的變數宣告都被提升至該函式的最上方
{% codeblock lang:js %}
var scope = "global";
function f() {
	console.log(scope);  // => "undefined", not "global"，因為scope被當成區域變數
	var scope = "local"; //變數在此設定初始值，但在函式中每個地方都有定義
	console.log(scope);  // => "local"
}
{% endcodeblock %}
以上程式等同如下
{% codeblock lang:js %}
var scope = "global";
function f() {
	var scope;           
	console.log(scope);  //尚未給初始值，所以是undefined
	scope = "local";     
	console.log(scope);  
}
{% endcodeblock %}

#### 因此在函式中宣告變數最好放到函式的最上方。


