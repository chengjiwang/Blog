---
title: Angular學習筆記 4 - 如何使用AngularFire
category: Angular
date: 2016-04-27 21:28:10
tags: Angular
---

## 1. Install AngularFire
為了使Angular和Firebase互相連動必須引入Firebase and AngularFire libraries

``` bash
<script src="https://cdn.firebase.com/js/client/2.2.4/firebase.js"></script>
<script src="https://cdn.firebase.com/libs/angularfire/1.2.0/angularfire.min.js"></script>
```
<!--more-->
## 2.Creating an Angular Module

Angular的module須設定firebase為相依的module

``` bash
var myApp = angular.module("myApp", ["firebase"]);
```

這樣設定可以讓我們透過Controller、Factory、Service存取$firebase的service($firebaseObject、$firebaseArray 、 $firebaseAuth services)

## 3.Creating a Controller

要在controller存取data，只要在controller裡注入(injecting)$firebase的service

``` bash
myApp.controller("MyController", ["$scope", "$firebaseArray",
        function($scope, $firebaseArray) {
          //Code here
        }
      ]);
```

## 4. Binding a Model to Firebase

建立Firebase reference，然後綁定 ng-model 和 Firebase 所對應的資料，在此是綁定Firebase URL上的資料到$scope.messages

``` bash
var ref = new Firebase("URL");
$scope.messages = $firebaseArray(ref);
```
## 5. Reading Data

當我們綁定Firebase URL到 model $firebaseObject 或 $firebaseArray ，Firebase就會和 model 產生連動，也就是當資料改變的時候，model 也會跟這更新。ng-repeat 是讓資料render出來。

``` bash
<ul id="example-messages" class="example-chat-messages">
  <li ng-repeat="msg in messages">
    <strong class="example-chat-username">{{ msg.from }}</strong>
    {{ msg.body }}
  </li>
</ul>
```

## 6. Writing Data

要將資料寫入$firebaseArray， 可以使用$firebaseArray的 $add()方法

``` bash
$scope.messages.$add({ from: name, body: $scope.msg });
```

## 參考文件：
1.[AngularFire Quickstart](https://www.firebase.com/docs/web/libraries/angular/quickstart.html)