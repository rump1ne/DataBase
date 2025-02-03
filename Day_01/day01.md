## Day 01 - Первые шаги работы с множествами и JOIN в SQL

## Упражнение 00 - Давайте заставим UNION танцевать

```sql
SELECT id AS object_id, pizza_name AS object_name FROM menu
UNION ALL
SELECT id AS object_id, name AS object_name FROM person
ORDER BY object_id, object_name;
```
![Screenshot 1](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/1.png)

## Упражнение 01 - UNION dance с подзапросом

```sql
SELECT 
  person.name AS object_name 
FROM 
  person 
UNION ALL 
SELECT 
  menu.pizza_name AS object_name 
FROM 
  menu 
ORDER BY 
  object_name;
```
![Screenshot 2](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/2.png)

## Упражнение 02 - Дубликаты или не дубликаты

```sql
SELECT 
  pizza_name 
FROM 
  menu 
UNION 
SELECT 
  pizza_name 
FROM 
  menu 
ORDER BY 
  pizza_name DESC;
```
![Screenshot 3](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/3.jpg)

## Упражнение 03 - "Скрытые" инсайты

```sql
SELECT order_date AS action_date, person_id FROM person_order
INTERSECT
SELECT visit_date AS action_date, person_id FROM person_visits
ORDER BY action_date ASC, person_id DESC;
```
![Screenshot 4](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/4.jpg)

## Упражнение 04 - Разница? Да, давайте найдем разницу между мультимножествами

```sql
SELECT person_id FROM person_order WHERE order_date = '2022-01-07'
EXCEPT ALL
SELECT person_id FROM person_visits WHERE visit_date = '2022-01-07';
```
![Screenshot 5](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/5.png)

## Упражнение 05 - Слышали ли вы о декартовом произведении?

```sql
SELECT 
  person.*, 
  pizzeria.* 
FROM 
  person, 
  pizzeria 
ORDER BY 
  person.id, 
  pizzeria.id
 ```
![Screenshot 6](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/1.jpg)

## Упражнение 06 - Давайте посмотрим на "Скрытые" Инсайты

```sql
SELECT order_date AS action_date, person.name 
FROM person_order
JOIN person ON person_order.person_id = person.id
INTERSECT
SELECT visit_date AS action_date, person.name 
FROM person_visits
JOIN person ON person_visits.person_id = person.id
ORDER BY action_date ASC, person.name DESC;
```
![Screenshot 7](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/7.jpg)

## Упражнение 07 - Просто сделайте JOIN

```sql
SELECT 
  order_date, 
  person.name || ('(age:') || age || (')') AS person_information 
FROM 
  person_order 
  JOIN person ON person_order.person_id = person.id 
ORDER BY 
  order_date ASC, 
  person_information ASC;
```
![Screenshot 8](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/8.jpg)

## Упражнение 08 - Перенос JOIN в NATURAL JOIN

```sql 
SELECT person_order.order_date, 
       CONCAT(person.name, ' (age:', person.age, ')') AS person_information
FROM person_order
NATURAL JOIN person
ORDER BY order_date, person_information;
```
![Screenshot 9](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/9.jpg)
## Упражнение 09 - IN против EXISTS

```sql
SELECT 
  name 
FROM 
  pizzeria 
WHERE 
  id NOT IN (
    SELECT 
      pizzeria_id 
    FROM 
      person_visits
  );



SELECT 
  pizzeria.name 
FROM 
  pizzeria 
WHERE 
  NOT EXISTS (
    SELECT 
      pizzeria_id 
    FROM 
      person_visits 
    WHERE 
      person_visits.pizzeria_id = pizzeria.id
  );
```
![Screenshot 10](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/10.jpg)

## Упражнение 10 - Глобальное JOIN

```sql 
SELECT person.name AS person_name, menu.pizza_name, pizzeria.name AS pizzeria_name
FROM person_order
JOIN menu ON person_order.menu_id = menu.id
JOIN pizzeria ON menu.pizzeria_id = pizzeria.id
JOIN person ON person_order.person_id = person.id
ORDER BY person_name, pizza_name, pizzeria_name;
```
![Screenshot 11](https://github.com/DenisShestakov1/data2sem/blob/main/day%2001/11.jpg)
