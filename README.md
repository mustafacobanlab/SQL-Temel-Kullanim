# 📓 Yazılımcılar İçin SQL Notları

Bu not, yazılımcıların işlerini görecek kadar bilmesi gereken SQL komutları, açıklamaları ve örnekleri içerir.  
Uygulama geliştirme süreçlerinde sıkça kullanılan sorgular ve yapıları özet halinde sunar.


---

# 📌 Temel SELECT ve Filtreleme

### Veri Çekme:

```sql
SELECT * FROM customers;
SELECT name, email FROM customers;
```

### Şartlı Veri Çekme:

```sql
SELECT * FROM products WHERE price > 100;
```

### Mantıksal Operatörler:

```sql
SELECT * FROM products WHERE price > 100 AND stock > 0;
SELECT * FROM users WHERE city = 'Ankara' OR city = 'İstanbul';
SELECT * FROM orders WHERE NOT status = 'Cancelled';
```

---

# 📌 Sıralama ve Kısıtlama

### ORDER BY:

```sql
SELECT * FROM products ORDER BY price ASC;
SELECT * FROM products ORDER BY price DESC;
```

### LIMIT ve OFFSET:

```sql
SELECT * FROM products LIMIT 10;
SELECT * FROM products LIMIT 10 OFFSET 20;
```

---

# 📌 JOIN İşlemleri

### INNER JOIN:

```sql
SELECT orders.id, customers.name
FROM orders
INNER JOIN customers ON orders.customer_id = customers.id;
```

### LEFT JOIN:

```sql
SELECT customers.name, orders.id
FROM customers
LEFT JOIN orders ON customers.id = orders.customer_id;
```

### RIGHT JOIN:

```sql
SELECT orders.id, customers.name
FROM orders
RIGHT JOIN customers ON orders.customer_id = customers.id;
```

### FULL OUTER JOIN:

```sql
SELECT * 
FROM orders
FULL OUTER JOIN customers ON orders.customer_id = customers.id;
```

---

# 📌 Gruplama ve Toplama

### GROUP BY:

```sql
SELECT city, COUNT(*) FROM users GROUP BY city;
```

### HAVING:

```sql
SELECT city, COUNT(*) AS total
FROM users
GROUP BY city
HAVING COUNT(*) > 10;
```

### Toplama Fonksiyonları:

```sql
SELECT COUNT(*) FROM orders;
SELECT SUM(price) FROM products;
SELECT AVG(price) FROM products;
SELECT MIN(price) FROM products;
SELECT MAX(price) FROM products;
```

---

# 📌 Alt Sorgular (Subqueries)

### SELECT İçinde:

```sql
SELECT name FROM products
WHERE price > (SELECT AVG(price) FROM products);
```

### FROM İçinde:

```sql
SELECT AVG(total_price)
FROM (SELECT SUM(price) AS total_price FROM orders GROUP BY customer_id) AS customer_totals;
```

---

# 📌 Veri Ekleme, Güncelleme ve Silme

### INSERT:

```sql
INSERT INTO users (name, email) VALUES ('Ahmet', 'ahmet@gmail.com');
```

### UPDATE:

```sql
UPDATE products SET price = 120 WHERE id = 5;
```

### DELETE:

```sql
DELETE FROM users WHERE id = 3;
```

---

# 📌 Veri Türleri ve PRIMARY KEY

### Tablonun Yapısı:

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

# 📌 BETWEEN, IN, LIKE

### BETWEEN:

```sql
SELECT * FROM products WHERE price BETWEEN 100 AND 500;
```

### IN:

```sql
SELECT * FROM users WHERE city IN ('Ankara', 'İstanbul');
```

### LIKE:

```sql
SELECT * FROM users WHERE name LIKE 'A%';
SELECT * FROM users WHERE email LIKE '%@gmail.com';
```

---

# 📌 CASE Kullanımı

### Koşullu Değer Döndürme:

```sql
SELECT name, 
  CASE 
    WHEN stock > 50 THEN 'Yüksek'
    WHEN stock BETWEEN 10 AND 50 THEN 'Orta'
    ELSE 'Düşük'
  END AS stok_durumu
FROM products;
```

---

# 📌 Index Kullanımı

### Performansı artırmak için:

```sql
CREATE INDEX idx_users_email ON users(email);
```

---

# 📌 NULL Kontrolü

### IS NULL:

```sql
SELECT * FROM users WHERE phone IS NULL;
```

### IS NOT NULL:

```sql
SELECT * FROM users WHERE phone IS NOT NULL;
```

---

# 📌 UNIQUE, NOT NULL, DEFAULT

### Kolon özellikleri:

```sql
CREATE TABLE categories (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

# 📌 Basit VIEW Oluşturma

### Sanal tablo (view) oluşturmak:

```sql
CREATE VIEW active_customers AS
SELECT * FROM customers WHERE active = true;
```

---

# 📌 Veritabanı ve Tablo Listeleme

### Veritabanları:

```sql
\l -- PostgreSQL
SHOW DATABASES; -- MySQL
```

### Tablolar:

```sql
\dt -- PostgreSQL
SHOW TABLES; -- MySQL
```



