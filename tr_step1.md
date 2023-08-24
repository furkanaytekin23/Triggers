Bu senaryoda sizlerden, size tahsis edilen makinelerde aşağıdaki talimatlar gereğince Linux komut satırında kullanıcının SQL sorgularını deneyebileceği şekilde gerekli komutların sağlandığı, "select join left" ve "select join right" işlemlerinin yapılması beklenmektedir.

Senaryo boyunca uygulama adımlarında belirtildiği şekilde SQL veritabanı tabloları oluşturulacak ve "select join left" ve "select join right" komutları yardımıyla sonuçların talimatlara uygun şekilde çıktılarının gözlemlenmesi istenmektedir.

### 🚀 Uygulama Adımları 🚀

1. Alpine Linux sisteminizde SQLite veritabanının kurulu olduğundan emin olunuz. Eğer kurulu değilse, Alpine Linux paket yöneticisi olan `apk` ile SQLite kurabilirsiniz. `apk add sqlite`
2. `/home/bb/` dizini altında `mydatabase.db` adında veritabanı dosyası oluşturunuz.
3. `sqlite3 mydatabase.db`komutunu girerek veritabanına bağlananın.
4. `.mode column` komutunu kullanarak sorgu sonuçlarını sütun düzeninde görüntülemeyi ayarlayın.
5. `.headers on` komutunu kullanarak sorgu sonuçlarında sütun başlıklarını görüntülemeyi ayarlayın.
6. Aşağıdaki SQL komutlarını kullanarak örnek tablo oluşturunuz.

```
CREATE TABLE customers (
    id INTEGER PRIMARY KEY,
    name TEXT,
    email TEXT
);

CREATE TABLE orders (
    id INTEGER PRIMARY KEY,
    customer_id INTEGER,
    product TEXT,
    amount REAL
);
```

7. Aşağıdaki SQL komutlarıyla da örnek verileri tablolara ekleyiniz.

```
INSERT INTO customers (name, email) VALUES ('Alice', 'alice@example.com');
INSERT INTO customers (name, email) VALUES ('Bob', 'bob@example.com');

INSERT INTO orders (customer_id, product, amount) VALUES (1, 'Product A', 100.0);
INSERT INTO orders (customer_id, product, amount) VALUES (1, 'Product B', 150.0);
INSERT INTO orders (customer_id, product, amount) VALUES (2, 'Product A', 200.0);

```

8. Müşteri adlarıyla beraber, müşteriye ait siparişleri sol birleştirme ile görüntülemek için aşağıdaki SQL sorgusunu giriniz.

```
SELECT customers.name, orders.product, orders.amount
FROM customers
LEFT JOIN orders ON customers.id = orders.customer_id;
```

9. Ürün isimleriyle beraber, siparişi veren müşterileri sağ birleştirme ile görüntülemek için aşağıdaki SQL sorgusunu giriniz.

```
SELECT customers.name, orders.product, orders.amount
FROM orders
RIGHT JOIN customers ON orders.customer_id = customers.id;
```

10. `.quit` komutunu kullanarak SQLite terminalinden çıkabilirsiniz.
