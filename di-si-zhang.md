---
description: 擷取Actions函式中的Calculations
---

# 第四章

### 函式的輸入與輸出

* 隱性輸入
  * 引數之外會使用到的變數，如：全域變數
* 隱性輸出
  * 除了回傳值外的變數，如：全域變數
* 顯性輸入
  * 引數
* 顯性輸出
  * 回傳值

```java
class CalculationPrice {
    private BigDecimal totalPrice = BigDecimal.ZERO;
    
    public BigDecimal sum(BigDecimal price) {
        this.totalPrice = this.totalPrice.add(price);
        return this.totalPrice;
    }
}
```

上述案例中可以看到有全域變數「totalPrice 」，而在methd sum中有引數「price」，回傳值是BigDecimal，邏輯是將全域變數「totalPrice 」與引數「price」進行相加。

其中totalPrice會被讀取也會被改變，但它是全域變數，因此屬於隱性輸入、隱性輸出，而price屬於顯性輸入，return 則屬於顯性輸出。

在進行重構之前需先釐清函式的輸入與輸出，目的是為了「消除隱性輸入與輸出」，消除隱性輸入與輸出的方式就是「移除全域變數」。

```java
class CalculationPrice {
    public BigDecimal sum(BigDecimal totalPrice, BigDecimal price) {
        totalPrice = totalPrice.add(price);
        return totalPrice;
    }
}
```

但這樣就可以了嗎？還記得FP有一個原則「參數不可變」，但上面的案例雖然消除了全域變數，但卻修改了引數「totalPrice」，所以還需要再進行調整。

```java
class CalculationPrice {
    public BigDecimal sum(BigDecimal totalPrice, BigDecimal price) {
        BigDecimal result = totalPrice.add(price);
        return result;
    }
}
```
