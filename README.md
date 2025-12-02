# goit-rdb-hw-03
# Домашнє завдання №3 — SQL (MySQL)

## Опис завдання
Перед виконанням домашнього завдання необхідно було завантажити 8 csv файлів з локального сховища, що успішно реалізовано (попередньо була створена окрема схема для виконання ДЗ)

## Створення схеми бази даних

```sql
CREATE SCHEMA IF NOT EXISTS hw_03;
USE hw_03;
```

---

<img width="217" height="216" alt="image" src="https://github.com/user-attachments/assets/2f18d32e-812b-49ee-a194-ccc994acc3dc" />


У межах домашнього завдання необхідно було написати та перевірити SQL-запити в **MySQL Workbench** для роботи з таблицями `products`, `shippers`, `suppliers`.

---

## 1. Вибір усіх стовпчиків із таблиці `products` та вибір колонок `name`, `phone` з таблиці `shippers`

### Запит 1.1 — Вибір усіх стовпчиків

```sql
SELECT * FROM products
LIMIT 10;
```

### Запит 1.2 — Вибір окремих колонок

```sql
SELECT 
    `name`,
    phone 
FROM shippers
LIMIT 10;
```

---

## 2. Середнє, максимальне та мінімальне значення колонки `price`

```sql
SELECT 
    AVG(price) AS avg_price,
    MAX(price) AS max_price,
    MIN(price) AS min_price
FROM products;
```

---

## 3. Унікальні значення `category_id` та `price`  
Сортування за спаданням `price`, обмеження 10 рядків

```sql
SELECT DISTINCT 
    category_id,
    price 
FROM products
ORDER BY price DESC
LIMIT 10;
```

---

## 4. Кількість продуктів у ціновому діапазоні від 20 до 100

```sql
SELECT 
    COUNT(`name`) AS count_products
FROM products
WHERE price > 20 AND price < 100;
```

---

## 5. Кількість продуктів та середня ціна у кожного постачальника

```sql
SELECT 
    sp.name AS supplier,
    COUNT(pr.`name`) AS count_products,
    ROUND(AVG(pr.price), 2) AS avg_price
FROM products AS pr
LEFT JOIN suppliers AS sp 
    ON sp.id = pr.supplier_id
GROUP BY sp.`name`;
```

---



---
