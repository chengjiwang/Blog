---
layout: post
title: Angular學習筆記1
category: Angular
date: 2016-04-10 09:54:41
tags: Angular
---

## Directives
* AngularJS是透過directives在HTML裡增加行為(behavior)。Directive是HTML標籤中的一個標記，
它使angular知道如何去調用JavaScript code。
* 如:當我們想要調用一個controller function，我們可以在HTML標籤裡增加一個ng-controller的屬性，並設定其值為function的名稱，就可以呼叫該function。

<!--more-->

## Getting Started
要開始使用Angular，首先我們需要再HTML裡引入Angular的libraries。

{% codeblock lang:html %}
<!DOCTYPE html>
<html ng-app>
  <head>
    <link rel="stylesheet" type="text/css" href="bootstrap.min.css" />
  </head>
  <body>
    <script type="text/javascript" src="angular.min.js"></script>
    <script type="text/javascript" src="app.js"></script>
  </body>
</html>
{% endcodeblock %}
## Modules(模組)

* Modules是寫AngularJS應用的程式片段，可以使程式分離開來，它可以讓我們的程式碼更好維護、可讀和測試。
* 模組可以定義自己的controllers、services、factories和directives。
* 模組也可以依賴其他模組做為相依性內容(dependencies)，因為我們可能在執行一個Module的時候，需要其相依的Modules。

### 1.建立Module

第一個引數是模組名稱，第二個引數是此模組相依的Modules。
``` bash
var app = angular.module('storeApp', [ ]);
```
### 2.載入現有模組

如果想載入已經由其他檔案定義的現有模組，可以只帶入第一個引數來完成。
``` bash
var app = angular.module('storeApp');
```

### 3.引入Module
* 在<code>&lt;html&gt;</code> 或 <code>&lt;body&gt;</code>標籤或其它元素中增加一個ng-app的directive，ng-app 有一個選擇性引數，可以使AngularJS以特定的模組作為應用程式的主要進入點。
* 當HTML文件被載入後，這個directive會執行storeApp這個Module，並產生一個Angular application。

## Expression
Expression可以讓我們將資料顯示到頁面上。

``` bash
<p> {{"hello" + " you"}}</p> 
```
如果我們在html輸入上面Expression，之後會render出 hello you。


## Controllers

* 可以幫助我們將應用內的資料顯示到頁面上。
* 透過定義函式和值，從而定義應用行為的地方。
* 它是 model 與 view 之間的閘道。

{% codeblock lang:js %}
(function(){
  var app = angular.module('store', [ ]);
  app.controller('StoreController', [ function(){
    this.product = gem;
  } ]);
  var gem= {
    name:'Dodecahedron',
    price: 2.54
  }
})();
{% endcodeblock %}
第一個引數是Controllers的名稱。必須是大寫
第二個引數是一個陣列，儲存此controller所有相依的內容，陣列中最後一個引數是controller函式。

ng-controller directive 會實體化一個controller實體，並附加在DOM元素中。
``` bash
<div ng-controller="StoreController as store">
```
controllerAs 語法，可以針對controller的每個實體給予一個名稱來識別實體在HTML中使用情形。
controllerAs 使用this 關鍵字來定義controller實體上的變數，並透過HTML的controller引用到這些變數。
這種語法優於較早之前的$scope作法。

## ng-show directive
ng-show directive 在expression的值為true時會顯示HTML元素。
(AngularJS 將true,非空字串,非零數字以及非空的物件都視為true)。

## ng-hide directive
ng-hide directive 在expression的值為true時會隱藏HTML元素 。

## ng-repeat directive
ng-repeat directive 可以瀏覽陣列或物件的(keys and values)，並把內容呈現在HTML中。

``` bash
ng-repeat="product in store.products"
```
store.products是我們要重複選取的array


