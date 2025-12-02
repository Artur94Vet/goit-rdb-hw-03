# goit-rdb-hw-03
# Домашнє завдання №3 — SQL (MySQL)

## Опис завдання
Перед виконанням домашнього завдання необхідно було завантажити 8 csv файлів з локального сховища, що успішно реалізовано (попередньо була створена окрема схема для виконання ДЗ)

## Створення схеми бази даних (Рисунок-1)
Використовуємо команду 'USE' для подальшої роботи з цільовою схемою  

```sql
CREATE SCHEMA IF NOT EXISTS hw_03;
USE hw_03;
```

---

*Рисунок-1: Створена схема та завантажені таблиці*  
<img width="217" height="216" alt="image" src="https://github.com/user-attachments/assets/2f18d32e-812b-49ee-a194-ccc994acc3dc" />


У межах домашнього завдання необхідно було написати та перевірити SQL-запити в **MySQL Workbench** для роботи з таблицями `products`, `shippers`, `suppliers`.

---

## 1. Вибір усіх стовпчиків із таблиці `products` та вибір колонок `name`, `phone` з таблиці `shippers`
Оператор `LIMIT` використовую ціленаправлено

### Запит 1.1 — Вибір усіх стовпчиків (Рисунок-2)

```sql
SELECT * FROM products
LIMIT 10;
```
*Рисунок-2*   
<img width="561" height="441" alt="image" src="https://github.com/user-attachments/assets/3969a274-ee4c-4191-97d8-f2e80d3e94c9" />

### Запит 1.2 — Вибір окремих колонок (Рисунок-3)

```sql
SELECT 
    `name`,
    phone 
FROM shippers
LIMIT 10;
```
*Рисунок-3*  
<img width="555" height="465" alt="image" src="https://github.com/user-attachments/assets/a051b7df-45d0-4d94-b70b-99c2d8204f98" />

---

## 2. Середнє, максимальне та мінімальне значення колонки `price`  (Рисунок-4)

```sql
SELECT 
    AVG(price) AS avg_price,
    MAX(price) AS max_price,
    MIN(price) AS min_price
FROM products;
```
*Рисунок-4*  
<img width="507" height="342" alt="image" src="https://github.com/user-attachments/assets/0ab4562d-5f6d-4556-ad1d-daf59fcde31d" />

---

## 3. Унікальні значення `category_id` та `price`  
Сортування за спаданням `price`, обмеження 10 рядків  (Рисунок-5)

```sql
SELECT DISTINCT 
    category_id,
    price 
FROM products
ORDER BY price DESC
LIMIT 10;
```
*Рисунок-5*  
<img width="374" height="484" alt="image" src="https://github.com/user-attachments/assets/fd5688c5-9dcc-4f3e-a11c-38d360cec73d" />

---

## 4. Кількість продуктів у ціновому діапазоні від 20 до 100  (Рисунок-6)

```sql
SELECT 
    COUNT(`name`) AS count_products
FROM products
WHERE price > 20 AND price < 100;
```
*Рисунок-6*  
<img width="443" height="308" alt="image" src="https://github.com/user-attachments/assets/72b614b0-6fbc-421a-80a7-e0440eaa8cd3" />

---

## 5. Кількість продуктів та середня ціна у кожного постачальника  (Рисунок-7)

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
*Рисунок-7*  
<img width="536" height="794" alt="image" src="https://github.com/user-attachments/assets/ee9801d3-0406-4721-a7a9-20238a609667" />

---
*При виконанні запитів оператори свідомо прописува у верхньому регістрі*



