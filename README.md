# sql
## 0
```sql
CREATE VIEW v_person_male AS (SELECT name FROM person WHERE gender = 'male');
CREATE VIEW v_person_female AS (SELECT name FROM person WHERE gender = 'female');
SELECT * FROM v_person_female
```
![image](https://github.com/reallyShould/sql/assets/77869589/f6d7b08c-c8b0-4cbd-84bb-16c82ae29bd7)

## 1
```sql
SELECT name FROM v_person_female
UNION
SELECT name FROM v_person_male
ORDER BY 1
```
![image](https://github.com/reallyShould/sql/assets/77869589/f94717b5-8d26-497b-a92e-2af8e46a3fa8)

## 2
```sql
CREATE VIEW v_generated_dates AS (
	SELECT dates::date as generated_date FROM generate_series('2022-01-01', '2022-01-31', interval '1 day') 
	AS dates
);
SELECT * FROM v_generated_dates
```
![image](https://github.com/reallyShould/sql/assets/77869589/55194602-2eb6-4784-a33a-9541c686a6ff)

## 3
```sql
SELECT * FROM v_generated_dates
EXCEPT
SELECT DISTINCT visit_date FROM person_visits WHERE visit_date BETWEEN '2022-01-01' AND '2022-01-31'
ORDER BY 1
```
![image](https://github.com/reallyShould/sql/assets/77869589/04f3b3fb-28d3-4516-8835-b5e3659cdbb9)

## 4
```sql

```

## 5 
```sql
CREATE VIEW v_price_with_discount AS (
	SELECT p.name, pi.name as pizza_name, m.price, m.price * 0.9 AS discount_price
	FROM person_order po
	JOIN person p ON p.id = po.person_id
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
  ORDER BY 1, 2, 3, 4
);
SELECT * FROM v_price_with_discount
```
![image](https://github.com/reallyShould/sql/assets/77869589/d36b0d54-d55e-4914-a916-d29080b937bd)

## 6
```sql
CREATE MATERIALIZED VIEW mv_dmitriy_visits_and_eats AS (
	SELECT pz.name FROM person_visits pv
	JOIN pizzeria pz ON pz.id = pv.pizzeria_id
	JOIN person p ON p.id = pv.person_id
	JOIN menu m ON m.pizzeria_id = pz.id
	WHERE p.name = 'Dmitriy' 
		  AND pv.visit_date = '2022-01-08' 
		  AND m.price < 800
);
SELECT * FROM mv_dmitriy_visits_and_eats
```
![image](https://github.com/reallyShould/sql/assets/77869589/0d52fda6-6d93-4689-9b2f-3b054b68a19b)

## 7
```sql
INSERT INTO person_visits 
VALUES (
	(SELECT MAX(id)+1 FROM person_visits),
	(SELECT id FROM person WHERE name = 'Dmitriy'),
	(SELECT pizzeria_id FROM menu WHERE price < 800 AND id != (SELECT id FROM pizzeria WHERE name = 'Papa Johns') LIMIT 1)
);
REFRESH MATERIALIZED VIEW mv_dmitriy_visits_and_eats;
SELECT * FROM person_visits
```
![image](https://github.com/reallyShould/sql/assets/77869589/0bddfb39-3ebe-4c5b-ade3-ecd3622eb2ee)

## 8
```sql
DROP VIEW v_person_female;
DROP VIEW v_person_male;
DROP VIEW v_generated_dates;
DROP VIEW v_price_with_discount;
DROP MATERIALIZED VIEW mv_dmitriy_visits_and_eats;
```
![image](https://github.com/reallyShould/sql/assets/77869589/e1000bf8-d33b-4289-973f-7ebb33b394aa)
