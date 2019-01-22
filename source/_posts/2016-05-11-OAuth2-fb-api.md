---
title: OAuth 2.0 - FB API筆記
date: 2016-05-11 14:38:17
category: OAuth 2.0
tags: OAuth 2.0
---

想要知道如何使用FB API，首先要知道OAuth 2.0。

## OAuth 2.0
OAuth 2.0 是一種允許Client代表Resource Owner存取資源的應用程式授權開放標準，他有4種角色。

* Resource Owner: 資料擁有者，也就是User。
* Client: 代表User去存取資料受保護資訊的應用程式，即APP。
* Resource Server: Client從這裡拿資料，即API
  1. 存放受保護資訊的伺服器
  2. 根據token來允許受保護資訊的請求
* Authorization Server: 在認證過Resource Owner，並在Resource Owner許可後，核發token。

<!--more-->

## 搭配 JavaScript SDK 使用「Facebook 登入」的步驟

### 1.檢查登入狀態: 確認使用者是否已經登入您的應用程式

使用 FB.getLoginStatus 來取得登入狀態，並儲存在 response 物件。

{% codeblock lang:js %}
FB.getLoginStatus(function(response) {
    statusChangeCallback(response);
});
{% endcodeblock %}

response 的物件中的內容如下：

{% codeblock lang:js %}
{
    status: 'connected',
    authResponse: {
        accessToken: '...',
        expiresIn:'...',
        signedRequest:'...',
        userID:'...'
    }
}
{% endcodeblock %}

### 2.如果使用者未登入，APP會向使用者要求一組資料存取權限。

藉由對 FB.login() 的呼叫，叫用「登入」對話方塊，並以 scope 參數向使用者要求權限。

{% codeblock lang:js %}
FB.login(function(response) {
   // handle the response
 }, {scope: 'public_profile,email'});
{% endcodeblock %}

瀏覽器會將使用者登入結果(是否已連結或取消)傳回給 APP，之後APP會將 authResponse 物件傳回至您進行 FB.login() 呼叫時所指定的Callback。

###  3.驗證用戶的身分。

如果您使用 Facebook 的 JavaScript SDK，系統會自動執行這些檢查，因此不用執行任何動作。

###  4.儲存所產生的存取權杖。

Facebook JavaScript SDK 會自動在瀏覽器中處理token儲存和登入狀態追蹤，要取得token，可以使用呼叫 FB.getLoginStatus() 傳回的 response 物件。

###  5. 進行 API 呼叫

在取得token後，APP就可代表使用者向API 拿取data。

使用 FB.api() 呼叫API 

{% codeblock lang:js %}
FB.api('/me', function(response) {
    console.log(JSON.stringify(response));
});
{% endcodeblock %}