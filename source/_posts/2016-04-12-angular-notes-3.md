---
title: Angular學習筆記3
category: Angular
date: 2016-04-12 14:16:28
tags: Angular
---

## ng-model directive

ng-model directive 用於輸入欄位中，會依 expression 的內容將使用者輸入的資料做處理。

{% codeblock lang:html %}
<input type="text" ng-model="name" placeholder="Enter your name">
{% endcodeblock %}
在此會將使用者輸入的內容值，儲存於name變數中

<!--more-->
## ng-submit directive

{% codeblock lang:html %}
 <form ng-submit="ctrl.submit()">
    <input type="text" ng-model="ctrl.user.username">
    <input type="password" ng-model="ctrl.user.password">
    <input type="submit" value="Submit">
  </form>
{% endcodeblock %}

在表單裡 ng-submit 有一些優點勝過按鈕的 ng-click，可以用多種方式觸發表單的提交事件(點擊按鈕或在input欄位按enter)，而 ng-click 只在點擊按鈕才會觸發。


## validation
* 要在表單中新增驗證功能，首先要在表單中使用novalidate去關閉HTML的預設驗證，
  主要是因為要使驗證有一致性。

* 如果有有必須填寫的欄位，可以使用required去限制

### 表單狀態
* $invalid : 當表單中任何驗證(required ,ng-minlength 及其他)有無效時，為true 。
* $valid 當表單中所有驗證都正確時，為true 。
* $pristine :表示表單尚未被使用者輸入或修改 。
* $dirty :表示使用者對欄位做了些動作 。

