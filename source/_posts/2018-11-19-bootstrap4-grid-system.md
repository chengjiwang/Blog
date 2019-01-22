---
layout: post
title: Bootstrap 4 網格系統
category: Bootstrap
date: 2018-11-19 14:39:45
tags: Bootstrap
---

## 網格選項
<!--more--> 
1. Class prefix
  `.col` :  全部寬度都套用
  `.col-sm` : 寬度超過 576 px 時套用
  `.col-md` : 寬度超過 768 px 時套用
  `.col-lg` : 寬度超過 992 px 時套用
  `.col-xl` : 寬度超過 1200 px 時套用
   
2. of columns : 預設總欄數為 12
3. Gutter width : 欄和欄的間距，預設是 30 px 。

## Bootstrap 中的欄與列
* 在使用網格系統時，必須使用容器在最外層，有分為`固定寬度(.container)`和`滿版寬(.container-fluid)`，一個基本的架構如下

``` html
<div class="container">
  <div class="row">
    <div class="col-md-6">item 1</div>
    <div class="col-md-6">item 2</div>
  </div>
</div>
```

* .col 的 padding  , 是為了製造 gutter width
``` css
.col {
  padding-right: 15px;
  padding-left: 15px;
}
```

* .row 的負 margin , 是為了補回外圍左右兩邊 .col 多的 padding 所造成的空白
``` css
.row {
  margin-right: -15px;
  margin-left: -15px;
}
```

