# test_task
Спроектировать схему БД.
<br>Модель данных реляционная.
<br>Сущности:
1. Номенклатура (наименование, кол-во, цена).
2. Каталог номенклатуры/Дерево категорий.
3. Клиенты (наименование, адрес).
4. Заказы покупателей.

<br>Ответ:

<img width="1237" height="714" alt="Снимок экрана от 2025-10-22 08-58-20" src="https://github.com/user-attachments/assets/1592be3f-aa4d-41c4-8d4f-6f461a5a59d2" />



Написать следующие SQL запросы:

2.1. Получение информации о сумме товаров заказанных под каждого клиента (Наименование клиента, сумма):

<pre>SELECT c.first_name, 
       c.last_name,
       SUM(o.quantity) as total_quantity
FROM orders o 
JOIN clients c ON o.client_id = c.client_id
GROUP BY c.client_id, c.first_name, c.last_name;</pre>




2.2. Найти количество дочерних элементов первого уровня вложенности для категорий
номенклатуры:

<pre>WITH tab AS (SELECT parent_id,
                    COUNT(parent_id) AS child_cats
             FROM categories
             GROUP BY parent_id)
SELECT name,
       IFNULL(child_cats, 0)
FROM categories c LEFT JOIN tab t ON c.cat_id = t.parent_id;<pre>
