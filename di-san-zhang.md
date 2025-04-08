---
description: 分辨Actions、Calaulations與Data
---

# 第三章

### 將函式思維應用在既存的程式碼

範例程式中，有幾個Actions呢？

```javascript
function main(affilliates) {
    affiliatePayout(affilliates);
}
function affiliatePayout(affilliates) {
    for(var a = 0; a < affilliates.lenth; a++) {
        figuarePayout[a];
    }
}
function figuarePayout(affilliate) {
    var owed = affilliate.sales * affilliate * commission;
    if (owed > 100)
        sendPayout(affilliate.bank_code, owed); //轉帳至帳戶
}
```

乍看之下會認為「sendPayout()」是Actions，但其實呼叫Actions的函式也屬於Actions，因此「sendPayout」、「figuarePayout」、「affiliatePayout」、「main」都屬於Actions，因為side effects是具有傳播性的，會一路往上層函式傳播。

### Actions的形式多變

* function calls
  * alert("") ->彈出警示交談窗
* Method calls
  * console.log(""); -> 在console中顯示資訊
* Constructors(建構元)
  * new Date();
* 刪除屬性
  * delete user.first\_name;
