---
title: JavaScript-ES6 基本介紹(下)
category: JavaScript
date: 2016-10-07 14:49:28
tags: [JavaScript, es6] 
---

# 4.1 - Arrays

<!--more-->

## array destructuring

* 使用 destructuring 將陣列裡多個值分配到區域變數。
* 可以將 destructuring 和 rest parameters combine 在一起 

{% codeblock lang:js %}
let users = ["Sam", "Tyler", "Brook"];

//舊寫法
let a= users[0];
let b= users[1];
let c= users[2];

//使用 array destructuring
let [a, b, c] = users;
console.log( a, b, c ); //Sam Tyler Brook

//值可以被discard
let [a, , b] = users;
console.log( a, b ); //Sam Brook

//Combining Destructuring With Rest Params
let [ first, ...rest ] = users;
console.log( first, rest ); //Sam ["Tyler", "Brook"]

{% endcodeblock %}

## for of

* for of 可以直接從陣列讀取每個元素，不須透過index 
* 物件不能使用for of ，因為 Symbol.iterator 屬性值不是 function 。

{% codeblock lang:js %}
let names = ["Sam", "Tyler", "Brook"];

for(let index in names){  //透過index
  console.log( names[index] ); 
}

for(let name of names){ //使用for of
  console.log( name ); 
}
{% endcodeblock %}

## Array.find

* Array.find 這個方法會將你傳入的測試函式， 回傳陣列中符合的第一個元素。

{% codeblock lang:js %}
let users = [
  { login: "Sam", admin: false },
  { login: "Brook", admin: true },
  { login: "Tyler", admin: true }
];

let admin = users.find( (user) => {
  return user.admin;
});
console.log( admin ); //{ "login" : "Brook", > "admin" : true }
{% endcodeblock %}

# 4.2 - Maps

## Map object 

* Map 物件是一個簡單的 key/value 資料結構，允許任何值去設定 key 或 value。當使用物件設定 key，並不會轉換成字串。

{% codeblock lang:js %}
let user1 = { name: "Sam" };
let user2 = { name: "Tyler" };

let totalReplies = new Map();
totalReplies.set( user1, 5 );//使用set方法
totalReplies.set( user2, 42 );

console.log( totalReplies.get(user1) );//5 ，使用get方法
console.log( totalReplies.get(user2) );//42
{% endcodeblock %}

## WeakMap

* WeakMap 只能用物件設定 key ，不能使用原始(Primitive)型別，如字串,數值。
* WeakMap 不能夠重複，因此不能使用在 for...of

# 4.3 - Sets

## Set object
* Set 物件儲存單一任何型態的值，不論是原始(Primitive)型別或物件。
* 重複的輸入值會被忽略。
* 可以和 for...of 或 array destructuring 一起使用


{% codeblock lang:js %}
let tags = new Set();

//use the add() method to add elements to a Set
tags.add("JavaScript");
tags.add("Programming");
tags.add({ version: "2015" });
tags.add("Web");
tags.add("Web");//重複的輸入值會被忽略

for(let tag of tags){
  console.log(tag);
}

let [a,b,c,d] = tags;
console.log(a, b, c, d);
{% endcodeblock %}

## WeakSet
* WeakSet 是 Set 的一個型態，只能允許物件的儲存。
* 不能使用在 for...of
* 不能從WeakSet 讀取值，但我們可以建立一個物件的 groups，然後確認某些物件是否有在這個 groups

{% codeblock lang:js %}
let weakTags = new WeakSet();

weakTags.add("JavaScript"); //TypeError: Invalid value > used in weak set
weakTags.add({ name: "JavaScript" });
{% endcodeblock %}

# 5.1 - Classes

## Class Syntax & constructor

* 使用class關鍵字，class 語法是 prototype 的語法糖
* constructor 是一個建立和初始物件的特殊方法。
* 設定在 constructor 裡的實例變數，可以被class內的其他實例方法所存取。

{% codeblock lang:js %}
class SponsorWidget {
  constructor(name, description, url){
    this.name = name;
    this.description = description;
	this.url = url;
  }

  render(){ //定義實例(instance )的方法
    let link = this._buildLink(this.url);
  }
}

let sponsorWidget = new SponsorWidget(name, description, url);
sponsorWidget.render();
{% endcodeblock %}

## Class Inheritance

* 子classes 繼承父 classes 的基本行為並有其特定的屬性 ，子classes 我們又稱為subclass
* extends 關鍵字會建立一個 class 繼承至另一個class的方法和屬性。 super 方法使子classes可以調用父class的設定的code

{% codeblock lang:js %}
class SponsorWidget extends Widget {
  constructor(name, description, url){
    super();
  }

  render(){
    let parsedName = this.parse(this.name);
  }
}
{% endcodeblock %}

# 5.2 - Modules Part I

* export 會將函式導出到模組系統
* default type 會以最簡單方式導出到模組系統
* 使用 import 載入模組

{% codeblock lang:js %}
//flash-message.js
export default function(message) {
  alert(message);
}

//app.js
import flashMessage from './flash-message';
flashMessage("Hello");
{% endcodeblock %}

* 多個函式要導出使用Named Exports

{% codeblock lang:js %}
//flash-message.js
export function alertMessage(message){
  alert(message);
}
export function logMessage(message){
  console.log(message);
}

//app.js
import { alertMessage, logMessage } from './flash-message';
alertMessage('Hello from alert');
logMessage('Hello from log');

{% endcodeblock %}

* 另外一種方式，將導入的整個模組當成一個物件，然後用物件的屬性去呼叫個別的函式

{% codeblock lang:js %}
//flash-message.js
export function alertMessage(message){
  alert(message);
}
export function logMessage(message){
  console.log(message);
}

//app.js
import * as flash from './flash-message';
flash.alertMessage('Hello from alert');
flash.logMessage('Hello from log');
{% endcodeblock %}


# 6.1 - Promises, Iterators, and Generators

## Promises

* Promises 可以使我們用更好的方式寫非同步程式碼，且不須使用 nested callbacks

*  當 Promises return 一個 Promise 物件時，並不是回傳一個結果，而是回傳一個 future value，如一個非同步操作的事件結果



request.onload = function() {
  if (request.status >= 200 && request.status < 400) {
    resolve(JSON.parse(request.response));
}
};
//...

Since request.response returns plain text
we'll go ahead and convert
it to JSON using JSON.parse.