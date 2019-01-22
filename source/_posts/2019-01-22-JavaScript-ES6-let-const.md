---
title: ES6 - let 與 const
category: JavaScript
date: 2019-01-22 11:55:09
tags: [JavaScript, es6] 
---

## const
  * const 是一個只能讀取，不能修改的常數
  * const 不能被重新赋值 
  <!--more--> 
  ``` js
  const satrs = 10;
  satrs = 5; // Uncaught TypeError: Assignment to constant variable
  ```

  * 宣告 const 時，必須赋值，否則會錯誤

  ``` js
  const satrs; // Uncaught TypeError: Missing initializer in const declaration
  satrs = 5; 
  ```

  * 物件內的屬性是可以重新指定，因為物件本身是傳參考，只要沒有將參考替換掉就是可以的。但無法重新指定成另一個物件，因為參考已經被替換。

  ``` js
  const Jason = { 
    hight: 170,
    wight: 65,
  };
  Jason.hight = 5; // 物件內的屬性是可以重新指定
  
  Jason = { 
    hight: 180,
    wight: 75,
  }; // 無法重新指定成另一個物件
  ```

## let 
  * let 可以被重新赋值

  ``` js
  let satrs = 10; 
  satrs = 5; 
  ```

  * let 在同一個scope內，不能重複宣告

  ``` js
  {
    let satrs = 10; 
    let satrs = 5; // Uncaught SyntaxError: Identifier 'satrs' has already been declared
  }
  ```

## let 與 const 無 hoisting

  * 使用 var 時，會有 hoisting 的問題

  ``` js
  console.log(sym); // undefined，記憶體已經準備好位置
  var sym = '三陽'; 

  ```

  * 使用 let 或 const，不會有 hoisting 的問題

  ``` js
  console.log(sym); // not defined 
  const sym = '三陽'; 

  ```

## scope 的不同

  var 的作用範圍是在 function scope
  let / const 的作用範圍是在 block scope

  ``` js
  // 1. 使用 var
  function printCarBrand () {
    var carBrand = 'Ford';
    if (true) {
      var carBrand = 'Skoda'; 
      console.log('inner:', carBrand); // Skoda
    }
    console.log('outside:', carBrand);  // Skoda
  }
  printCarBrand();

  // 2. 使用 let
  function printCarBrand () {
    const carBrand = 'Ford';
    if (true) {
      const carBrand = 'Skoda';
      console.log('inner:', carBrand);  // Skoda
    }
    console.log('outside:', carBrand);  // Ford
  }
  printCarBrand();

  ```