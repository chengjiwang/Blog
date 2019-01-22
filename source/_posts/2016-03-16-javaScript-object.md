---
layout: post
title: JavaScript - 物件
category: JavaScript
date: 2016-03-16
tags:  JavaScript
---

物件是屬性(property)所構成的一個集合。每個屬性皆具有一個名稱(name)與一個值(value)。

# 一.建立物件字面(object literal)

為物件加上一個變數宣告，然後在{ }裡加入屬性，屬性間需以逗號分開，最後一個屬性不需要逗號。

<!--more-->

``` bash
var dog = {
  name: "snoopy",
  breed: "Beagle",
  weight: 20
}
```
# 如何操作屬性

### 1.  存取(access)物件的屬性

``` bash
dog.name  //使用點號的方式
dog["name"] //使用方括號的方式
```

### 2.  如何改變一個屬性
將一個新值賦值給該屬性。

``` bash
dog.weight= 25; //weight的值會變成25
```

### 3.  如何添加新的屬性
指定新的屬性並對它賦值

``` bash
dog.owner= "Charlie Brown";
```
### 4.  刪除屬性
使用delete。 屬性刪除成功，delete運算式會傳回true。

``` bash
delete dog.owner;
```

## 物件傳遞給函式
物件是按reference傳遞(pass-by-reference)，所以當你叫用一個函式並把一個物件傳遞給它時，
你所傳遞的是物件reference，這代表著，如果你在函式中改變物件的屬性，會因而改變原本物件的屬性。

## 物件的方法(method)
{% codeblock lang:js %}
var dog = {
  name: "snoopy",
  model: "Beagle",
  weight: 20
  bark: function(){
	alert(woof);
  }
}
{% endcodeblock %}
物件裡的函式稱為方法(method)，要呼叫物件的方法，還是要用點號。
如 dog.bark();


# 二.物件建構程序(object constructor)

當有大量的物件須建立時，我們可以使用另一種方法建立物件，就是物件建構程序(object constructor)
建構程序的過程分為兩個步驟: 首先定義建構程序函式(名稱通常以大寫開頭)，接著用它來建立物件。

{% codeblock lang:js %}
function Dog(name,breed,weight){
  this.name = name ; //this 指的是新建立的物件
  this.breed = breed ;
  this.weight = weight;
}
var snoopy = new Dog("snoopy","Beagle",20);
{% endcodeblock %}


### 建構程序函式引數改成物件字面
{% codeblock lang:js %}
var snoopyParams = {
  name: "snoopy",
  breed: "Beagle",
  weight: 20
}

var snoopy = new Dog(snoopyParams);

function Dog(Params){
  this.name =  Params.name ;
  this.breed = Params.breed ;
  this.weight = Params.weight;
}
{% endcodeblock %}

### instanceof
instanceof 可用於確定某個物件是否為特定建構程序的一個實例。
{% codeblock lang:js %}
if(snoopy instanceof Dog){	
}
{% endcodeblock %}