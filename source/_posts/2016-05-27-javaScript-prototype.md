---
title: JavaScript - Prototype
category: JavaScript
date: 2016-05-27 17:45:49
tags: JavaScript
---

## 原型(prototype)
* 物件可以從其他物件繼承屬性和行為，也就是原型繼承(prototype inheritance)，被繼承的物件就是原型。

* 我們會把通用的屬性放在原型裡，專屬的屬性放在物件實例裡。

* 如果我們在物件實例叫用一個屬性，會先在物件裡尋找，如果無法找到，才會到原型去尋找。

<!--more-->

以下程式碼每個物件都有bark方法的一個副本，會造成資源影響，要解決這個問題可以使用原型。

{% codeblock lang:js %}
function Dog(name, breed, weight) {
	this.name = name;
	this.breed = breed;
	this.weight = weight;
	this.bark = function() {
		if (this.weight > 25) {
			alert(this.name + " says Woof!");
		} else {
			alert(this.name + " says Yip!");
		}
	};
}

var fido = new Dog("Fido", "Mixed", 38);
var fluffy = new Dog("Fluffy", "Poodle", 30);
var spot = new Dog("Spot", "Chihuahua", 10);
{% endcodeblock %}

## 設置原型
* 透過建構程序的prototype屬性來存取原型
* 只要我們新增一個屬性到原型，任何繼承該原型物件都可以使用該屬性。
{% codeblock lang:js %}
function Dog(name, breed, weight) {
	this.name = name;
	this.breed = breed;
	this.weight = weight;
}

Dog.prototype.bark = function() {
	if (this.weight > 25) {
		alert(this.name + " says Woof!");
	} else {
		alert(this.name + " says Yip!");
	}
};
var fido = new Dog("Fido", "Mixed", 38);
var fluffy = new Dog("Fluffy", "Poodle", 30);
var spot = new Dog("Spot", "Chihuahua", 10);
{% endcodeblock %}

## 覆寫原型
雖然我們從原型繼承某些屬性，但我們還是可以覆寫屬性，只要在物件裡新增屬性即可。

{% codeblock lang:js %}
spot.bark = function() {
	console.log(this.name + " says WOOF!");
};
{% endcodeblock %}

## hasOwnProperty
物件的 hasOwnProperty 方法可以判斷屬性是位於物件(回傳true)或是原型(回傳false)。

{% codeblock lang:js %}
Dog.prototype.species= 'canine';
spot.hasOwnProperty("species"); //回傳false，因為species定義於原型，而非spot物件
{% endcodeblock %}

## 原型鏈(chain of prototypes)

* 一個物件並非只能從原型繼承屬性，也可以從原型所構成的原型鏈繼承屬性。
* 原型鏈就是一個原型繼承自另一個原型(在此為 Dog prototype)。

### 建立繼承自Dog prototype 的原型

新增一個建構程序，將它的prototype屬性設定為一個新的物件實例，並設定constructor屬性
{% codeblock lang:js %}
function ShowDog(name, breed, weight, handler) {
	this.name = name;
	this.breed = breed;
	this.weight = weight;
	this.handler = handler;
}
ShowDog.prototype = new Dog();
ShowDog.prototype.constructor = ShowDog;
{% endcodeblock %}

之後就可以對ShowDog.prototype 新增一些屬性，和建立ShowDog的物件實例

{% codeblock lang:js %}
ShowDog.prototype.bait = function() {
	console.log("Bait");
};
var scotty = new ShowDog("Scotty", "Scottish Terrier", 15, "Cookie");
{% endcodeblock %}


 
