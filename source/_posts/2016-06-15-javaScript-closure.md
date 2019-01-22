---
title: JavaScript-Closure
date: 2016-06-15 22:08:44
category: JavaScript
tags: JavaScript
---

js 使用語彙scope，這表示函式執行時使用的變數scope是函式定義生效的scope，而非調用時的變數scope

{% codeblock lang:js %}
var scope = "global scope"; // A global variable
function checkscope() {
	var scope = "local scope"; // A local variable
	function f() {
		return scope; 
	} 
	return f();
}
checkscope() // => "local scope"
{% endcodeblock %}

<!--more-->
上面的checkscope() 宣告區域變數，定義並調用一個回傳該變數值的函式，根據語彙scope 我們會檢視最接近的外層函式的變數值
所以會回傳"local scope"

{% codeblock lang:js %}
var scope = "global scope"; // A global variable
function checkscope() {
	var scope = "local scope"; // A local variable
	function f() { 
		return scope; 
	} 
	return f;
}
checkscope()() // What does this return?
{% endcodeblock %}

這次我們改寫checkscope() ，直接回傳了函式f 本身。

根據語彙scope規則: 函式執行時使用的 scope chain ，是定義時生效的 scope chain 。

f() 定義時的scope chain，變數是繫結至 "local scope"，就算函式 f() 被執行時仍然有效。

所以會回傳 "local scope" 而不是 "global scope"。

由上述可知 Closure 會捕抓它們外層函式(即它們定義之處)的區域變數之繫結。

## 參考文件：
1. JavaScript: The Definitive Guide ，By David Flanagan