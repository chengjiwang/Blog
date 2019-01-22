---
title: Angular學習筆記2
category: Angular
date: 2016-04-11 14:42:56
tags: Angular
---


## Filter

Angular有很多的filter(如date、 uppercase & lowercase 、limitTo、orderBy...等)，但其都是依照以下的方式運作，將拿取的資料傳給filter

``` bash
{{ data | filter:options }}

```
pipe( | ) 會將data輸出到後面的filter

<!--more-->
### 1.currency filter: 會列印出正確的金錢符號和小數點位數
 
``` bash
{{product.price | currency }}
```

### 2.uppercase & lowercase filter: 變更為大/小寫

``` bash
{{'octagon gem' | uppercase}} 
=>  OCTAGON GEM
```

### 3.limitTo filter: 可用來控制輸出的個數

``` bash
<li ng-repeat="product in store.products | limitTo:3">
=> 只會輸出前3個product
```

### 4.orderBy filter: 可用來排序輸出

``` bash
<li ng-repeat="product in store.products | orderBy:'-price'">
=> 對product 依價格從高到低排序輸出

```
### 5. data filter: 顯示時間的格式

``` bash
{{'1388123412323' | date:'MM/dd/yyyy @ h:mma'}}

```

## ng-src directive
  
可用來顯示圖片
``` bash
<img ng-src="{{product.images[0]}}"/>
=> 顯示product的第1筆圖片
```

## ng-click directive
ng-click directive 是當有ng-click 事件發生的時候，會去執行expression的內容。

``` bash
<ul>
  <li> <a href ng-click="tab = 1"> Description</a> </li>
  <li> <a href ng-click="tab = 2"> Specifications</a> </li>
  <li> <a href ng-click="tab = 3"> Reviews</a> </li>
</ul>
{{tab}}

```
在此對 ng-click directive賦值，如tab = 1，所以當我們按下第一個tabs時，tab值等於1。
如果要讓tab的值顯示在頁面上，可以使用 tab expression。
當ng-click 改變 tab值，tab expression也會跟著改變，我們稱這為2-way Data Binding。


## ng-bind directive

* 與雙大括號expression相同，可取出controller的值，並在view 顯示出來，同時也會維持資料的綁定和更新。
* 但是ng-bind 優點多於雙大括號，可以避免AngularJS載入時雙大括號會發生殘影的問題。

## ng-init directive

ng-init directive允許我們在當前的scope裡對expression設定初始值。

``` bash
ng-init="tab = 1"
=> 代表初始化值為tab = 1
```

## ng-class directive

* ng-class directive 用來選擇性地套用與移除元素的css。
* ng-class 可以用字串或物件作為內容值，如果它是個字串，就直接套用css。
  如果是個物件(從controller裡的函式回傳)，AngularJS 會根據物件values 為 true 或 false ,來套用或移除css。

``` bash
ng-class="{ active:tab === 1 }"
```
設定class的name(在此為active)，之後是一個expression賦值，如果expression為true，會新增active的class。


