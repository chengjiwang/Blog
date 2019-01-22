---
title: JavaScript-ES6 基本介紹(上)
category: JavaScript
date: 2016-10-03 16:22:09
tags: [JavaScript, es6] 
---

# 1. let & const

<!--more-->

## let

* let的變數只在其宣告的block內有效。
{% codeblock lang:js %}
if {
  let a= 10;
} else {
  var b= 5;
}

a // ReferenceError: a is not defined.
b // 5
{% endcodeblock %}

* 不存在hoisting
let不像var那樣會發生提升現象。

* let 在同一個scope內，不能重複宣告，但可以重新赋值
{% codeblock lang:js %}
{
  let b = 10;
  let b = 5; //TypeError
  b = 7 ; // b=7
}
{% endcodeblock %}

## const
* const 是一個只能讀取，不能修改的常數
* 不能對已經赋值的const，再一次赋值。
{% codeblock lang:js %}
const users =10;
users = 5 ; //syntax error
{% endcodeblock %}

* 宣告const 時，必須赋值，否則會錯誤
{% codeblock lang:js %}
const users ; //syntax error
users=10;
{% endcodeblock %}

* const 和 let 一樣，只在其宣告的block內有效。

# 2.1 default parameter & named parameters

## default parameter values: 設定參數的預設值

當函式內有參數的述句時， 如果在呼叫函式時，沒有給予參數，會產生錯誤。
{% codeblock lang:js %}
function loadProfiles(){
  let namesLength = userNames.length;
  console.log(namesLength);
}

loadProfiles(); //TypeError: Cannot read property 'length' of undefined
{% endcodeblock %}

這時候，可以設定參數的預設值，避免發生錯誤。
當函式呼叫時，如果沒有傳入參數，就會使用預設值。
{% codeblock lang:js %}
function loadProfiles(userNames = []){
  let namesLength = userNames.length;
  console.log(namesLength);
}

loadProfiles(); //0
{% endcodeblock %}

## named parameters

{% codeblock lang:js %}
function setPageThread(name, options = {}){
  let popular = options.popular;
  let expires = options.expires;
  let activeClass = options.activeClass;
//...
}

setPageThread("New Version out Soon!", {
  popular: true,
  expires: 10000,
  activeClass: "is-page-thread"
});
{% endcodeblock %}

使用 named parameters 幫助我們了解 Options Object 如何被調用。
{% codeblock lang:js %}
function setPageThread(name, { popular, expires, activeClass }){
  console.log("Name: ", name);
  console.log("Popular: ", popular);
  console.log("Expires: ", expires);
  console.log("Active: " , activeClass);
}

setPageThread("New Version out Soon!", {
  popular: true,
  expires: 10000,
  activeClass: "is-page-thread"
});
{% endcodeblock %}

# 2.2 rest parameters & spread operator & arrow function
##  rest parameters

* 允許我們將不明確的參數個數作為一個明確的 array 參數使用
* 使用(...) 語法 ，將我們傳入函式的參數當成 array

{% codeblock lang:js %}
function displaytags(...tags){
  for(let i in tags){
    let tag = tags[i];
    _addToTopic(target, tag);
  }
}
{% endcodeblock %}

## spread operator

* 允許我們分裂一個參數的陣列成為個別的元素。

* 和 rest parameters 很類似，都是使用(...) 語法，但 spread operator 使用在函數調用，而非定義的時候。

{% codeblock lang:js %}
getRequest("/topics/17/tags", function(data){
  let tags = data.tags;
  displayTags(...tags); //接受個別的元素，而非陣列
})
{% endcodeblock %}

## arrow function

* arrow function 又被稱為lexical 綁定，因其將作用域綁定於定義的時候，而非執行的時候。

{% codeblock lang:js %}
function TagComponent(target, urlPath){
  this.targetElement = target;
  this.urlPath = urlPath;
}

TagComponent.prototype.render = function(){
  getRequest(this.urlPath,(data) => {
    let tags = data.tags;
    displayTags(this.targetElement, ...tags); //this 和 TagComponent 作用域綁定一起
  });
}
{% endcodeblock %}

# 3.1 - Objects and Strings

## Object Initializer Shorthand

* 當物件屬性的 name 和 value 相同時，我們可以移除重複的變數名稱
* 將變數分配到物件的屬性

{% codeblock lang:js %}
let name = "Sam";
let age = 45;
let friends = ["Brook","Tyler"];

let user = { name: name, age: age, friends: friends };

let user = { name, age, friends }; //使用 Object Initializer Shorthand
{% endcodeblock %}

## Object Destructuring

* 使用 shorthand 將屬性從物件用相同名稱分配到區域變數。
* 不一定要將所有的物件都做分配，可以選擇需要的即可。

{% codeblock lang:js %}
function buildUser(first, last){
  let fullName = first + " " + last;
  return { first, last, fullName };
}
let user = buildUser("Sam", "Williams");

//之前寫法，需重複賦值給變數
let first = user.first; 
let last = user.last;
let fullName = user.fullName;

//使用 Object Destructuring ，自動將函式 return 的物件，分配到first, last 和 fullName 區域變數
let { first, last, fullName } = buildUser("Sam", "Williams");

//當只需從 return object 中獲取 last 和 fullName
let { last, fullName } = buildUser("Sam", "Williams"); 
{% endcodeblock %}


## Method Initializer Shorthand

{% codeblock lang:js %}
//之前的js版本，物件方法的寫法
{
  first,
  last,
  fullName,
  isActive: function(){
	return postCount >= ACTIVE_POST_COUNT;
}

//使用 Method Initializer Shorthand
{
  first,
  last,
  fullName,
  isActive(){
	return postCount >= ACTIVE_POST_COUNT;
}
{% endcodeblock %}

## template strings

* template strings 對於 string interpolation 更方便，並有 Multi-line Strings 的功能。
{% codeblock lang:js %}
let fullName = first + " " + last; // 之前寫法

let fullName = `${first} ${last}`; // 使用$和{}符號
{% endcodeblock %}

# 3.2 - Object.assign

* 這個方法會將多個來源物件的屬性複製到目標物件(第一個參數)
* 因為是複製到新的物件，所以不會改變原始物件

{% codeblock lang:js %}
let settings = Object.assign({}, defaults, options);
{% endcodeblock %}