---
description: 改良Actions的設計
---

# 第五章

### 「拆解」是設計的本質

* 可重複使用性提升
* 維護更方便
* 測試更簡單

```java
@Getter
@AllArgsConstructor
class Product {
    private String _name;
    private BigDecimal _price;
}

class ShoppingCart {
    public List<Product> addProduct(List<Product cart, String _name, BigDecimal _price) {
        List<Product> newCart = new ArrayList<>(cart);
        newCart.add(new Product(_name, _price));
        return newCart;
    }
    
    public void main(String[] args) {
        List<Product> cart = new ArrayList<>();
        cart = addProduct(cart, "麥香奶茶", new BigDecimal("10"));
        cart = addProduct(cart, "麥香紅茶", new BigDecimal("10"));
        cart = addProduct(cart, "麥香綠茶", new BigDecimal("10"));
    }
}
```

addProduct乍看之下只做了新增產品這件事，但其實是做了4件事情

* 複製陣列 -> List newCart = new ArrayList<>(cart)
* 建立產品資訊 -> new Product(\_name, \_price)
* 將產品資訊放入陣列中 -> newCart.add()
* 回傳新的購物車資訊 -> return newCart

接著嘗試將這些邏輯拆解

```java
@Getter
@AllArgsConstructor
class Product {
    private String _name;
    private BigDecimal _price;
}

class ShoppingCart {
    public List<Product> addProduct(List<Product cart, Product product) {
        return addProduct(cart, product);
    }
    
    private List<Product> addProduct(List<Product cart, Product product) {
        List<Product> newCart = new ArrayList<>(cart);
        newCart.add(product);
        return newCart;
    }
    
    private Product genProduct(String _name, BigDecimal _price) {
        return new Product(_name, _price);
    }
    
    public void main(String[] args) {
        List<Product> cart = new ArrayList<>();
        cart = addProduct(cart, genProduct("麥香奶茶", new BigDecimal("10")));
        cart = addProduct(cart, genProduct("麥香紅茶", new BigDecimal("10")));
        cart = addProduct(cart, genProduct("麥香綠茶", new BigDecimal("10")));
    }
}
```

將邏輯拆解之後再來就是把邏輯通用化

```java
@Getter
@AllArgsConstructor
class Product {
    private String _name;
    private BigDecimal _price;
}

class ShoppingCart {
    public List<Product> addProduct(List<Product cart, Product product) {
        return addProduct(cart, product);
    }
    
    private List<Product> addProduct(List<Product cart, Product product) {
        List<Product> newCart = new ArrayList<>(cart);
        newCart.add(product);
        return newCart;
    }
    
    private Product genProduct(String _name, BigDecimal _price) {
        return new Product(_name, _price);
    }
    
    public void main(String[] args) {
        List<Product> cart = new ArrayList<>();
        cart = addProduct(cart, genProduct("麥香奶茶", new BigDecimal("10")));
        cart = addProduct(cart, genProduct("麥香紅茶", new BigDecimal("10")));
        cart = addProduct(cart, genProduct("麥香綠茶", new BigDecimal("10")));
    }
}


```
