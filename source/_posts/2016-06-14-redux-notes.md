---
title: Redux 筆記
date: 2016-06-14 22:13:16
category: React
tags: [React, Redux] 
---

## 三大原則
#### 1.唯一真相來源(Single source of truth)
整個應用程式的 state，被儲存在一個樹狀物件放在唯一的 store 裡面。

#### 2.State 是唯讀的(State is read-only)
改變 state 的唯一的方式是發出一個 action，也就是一個描述發生什麼事的物件。

#### 3.變更被寫成 pure functions (Changes are made with pure functions)

* 要指定 state tree 如何藉由 actions 來轉變，你必須撰寫 pure reducers。

* 它取得先前的 state 和一個 action，並回傳下一個 state。請記得要回傳一個新的 state 物件，而不要去改變先前的 state。

<!--more-->

## Actions

* Actions 是一個物件 (plain object)。
* Actions 必須有一個 type 屬性，它代表被執行的 action 的類型。
* Actions 是從你的應用程式傳遞資料到你的 store 的資訊 payloads，藉由 store.dispatch() 來把它們傳遞到 store。

{% codeblock lang:js %}
const ADD_TODO = 'ADD_TODO'
{
  type: ADD_TODO,
  text: 'Build my first Redux app'
}
{% endcodeblock %}


## Action Creators
Action creators 是一個產生 actions 的 functions，它會回傳一個 action 物件。

{% codeblock lang:js %}
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}
{% endcodeblock %}

使用dispatch 將action 傳給Reducers
```js
dispatch(addTodo(text))
```

## Reducers
* 指定應用程式的 state 要如何去應對改變。
* reducer 是一個 pure function，會接收 原本的狀態 (state)，與 改變原本狀態的參數 (Action)，然後回傳改變後的狀態 (state)。

```js
function visibilityFilter(state = SHOW_ALL, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return action.filter
    default:
      return state
  }
}
```

## Store
* Redux 應用程式中將只會有一個 store ，它是由所有的 Reducer (與 Middleware) 所組成 ，掌管應用程式狀態

### 建立 store 
{% codeblock lang:js %}
import { createStore } from 'redux'
import todoApp from './reducers'
let store = createStore(todoApp)
{% endcodeblock %}

