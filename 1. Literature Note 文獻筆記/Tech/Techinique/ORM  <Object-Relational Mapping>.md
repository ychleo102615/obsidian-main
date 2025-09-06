物件
```
public class Product {
	private Long id;
	private String name;
	private Integer remain;
public Product() {
}
public Product(Long id, String name, Integer remain) {
	this.id = id;
	this.name = name;
	this.remain = remain;
}
/* getter and setter ... */
}
```

資料庫
```
+---------------------+
|       Product       |
+====+=======+========+
| ID | NAME  | REMAIN |
+----+-------+--------+
| 1  | apple | 10     |
+----+-------+--------+
| 2  | book  | 15     |
+----+-------+--------+
```

這兩者的關係就是「物件關係映射」

[參考](https://medium.com/learning-from-jhipster/13-%E7%94%9A%E9%BA%BC%E6%98%AF-jdbc-orm-jpa-orm%E6%A1%86%E6%9E%B6-hibernate-c762a8c5e112)
