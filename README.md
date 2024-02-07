# sql
## 0
```sql
WITH m AS (SELECT * FROM menu WHERE price BETWEEN 800 AND 1000)
SELECT m.pizza_name, m.price, pz.name as pizzeria_name, pv.visit_date, p.name FROM person_visits pv
JOIN pizzeria pz
	ON pz.id = pv.pizzeria_id
JOIN person_order po
	ON po.person_id = pv.person_id
JOIN person p
	ON p.id = po.person_id
JOIN m 
	ON m.pizzeria_id = pv.pizzeria_id
WHERE p.name = 'Kate'
ORDER BY 1, 2, 3
```
![image](https://github.com/reallyShould/sql/assets/77869589/e0fa5faf-fa60-44c7-b207-6e5e95bdfe19)

## 1
```sql
SELECT id as menu_id FROM menu
WHERE id NOT IN (SELECT menu_id FROM person_order)
```
![image](https://github.com/reallyShould/sql/assets/77869589/d3c8d85b-786f-46a7-9daa-bc8368641035)

## 2
```sql
SELECT menu.pizza_name, menu.price, pizzeria.name as pizzeria_name FROM menu
JOIN pizzeria
	ON pizzeria.id = menu.pizzeria_id
WHERE menu.id NOT IN (SELECT menu_id FROM person_order)
ORDER BY 1, 2
```
![image](https://github.com/reallyShould/sql/assets/77869589/768db024-7fc6-4ebb-aafd-cf3f05419c14)

## 3


## 4


## 5
```sql
WITH andrey_visits AS (
	SELECT pi.name, pv.visit_date, pi.id FROM person_visits pv
	JOIN pizzeria pi ON pi.id = pv.pizzeria_id
	JOIN person p ON p.id = pv.person_id
	WHERE p.name = 'Andrey' 
), andrey_orders AS (
	SELECT pi.name, po.order_date, pi.id FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	JOIN person p ON p.id = po.person_id
	WHERE p.name = 'Andrey'
)

SELECT av.name FROM andrey_visits av
LEFT JOIN andrey_orders ao ON av.id = ao.id
WHERE ao.name IS NULL
```
![image](https://github.com/reallyShould/sql/assets/77869589/da1bf666-5ac1-4695-8702-e6be4c99c4bd)

## 6
```sql
SELECT m1.pizza_name, pz1.name as pizzeria_name_1, pz2.name as pizzeria_name_2, m1.price FROM menu m1
JOIN menu m2 ON m1.pizza_name = m2.pizza_name and m1.price = m2.price
JOIN pizzeria pz1 ON pz1.id = m1.pizzeria_id
JOIN pizzeria pz2 ON pz2.id = m2.pizzeria_id
WHERE pz1.name < pz2.name
```
![image](https://github.com/reallyShould/sql/assets/77869589/448915c1-1dcc-4ca5-87ae-23cc172953a1)

## 7 
```sql
INSERT INTO menu
VALUES (19, 2, 'greek pizza', 800);
```
![image](https://github.com/reallyShould/sql/assets/77869589/8806e4ad-11e7-4478-b9ca-cfa89c0ed0cd)

## 8 
```sql
INSERT INTO menu
VALUES ((SELECT max(id) + 1 FROM menu), 2, 'sicilian pizza', 900);
```
![image](https://github.com/reallyShould/sql/assets/77869589/79b655df-7e2a-4b9e-9199-4c4142a99fa9)

## 9
```sql
INSERT INTO person_visits
VALUES (
	(SELECT max(id) + 1 FROM person_visits),
	(SELECT id FROM person WHERE person.name = 'Denis'),
	(SELECT id FROM pizzeria WHERE pizzeria.name = 'Dominos'),
	'2022-02-24'
);
INSERT INTO person_visits
VALUES (
	(SELECT max(id) + 1 FROM person_visits),
	(SELECT id FROM person WHERE person.name = 'Irina'),
	(SELECT id FROM pizzeria WHERE pizzeria.name = 'Dominos'),
	'2022-02-24'
);
SELECT * FROM person_visits
```
![image](https://github.com/reallyShould/sql/assets/77869589/561d3b78-9dfa-4803-9b07-4d7f27f195d4)

## 10
```sql
INSERT INTO person_order
VALUES (
	(SELECT max(id) + 1 FROM person_order),
	(SELECT id FROM person WHERE person.name = 'Denis'),
	(SELECT id FROM menu WHERE menu.pizza_name = 'sicilian pizza'),
	'2022-02-24'
);
INSERT INTO person_order
VALUES (
	(SELECT max(id) + 1 FROM person_order),
	(SELECT id FROM person WHERE person.name = 'Irina'),
	(SELECT id FROM menu WHERE menu.pizza_name = 'sicilian pizza'),
	'2022-02-24'
);
SELECT * FROM person_order
```
![image](https://github.com/reallyShould/sql/assets/77869589/344394b0-2bfd-47d8-ac99-d33cbb04ea96)

## 11
```sql
UPDATE menu
SET price = price - price * 0.1
WHERE menu.pizza_name = 'greek pizza';
SELECT * FROM menu
```
![image](https://github.com/reallyShould/sql/assets/77869589/07ba24d9-5df7-4598-9ed9-7598d8f8cee8)

## 12
```sql

```

