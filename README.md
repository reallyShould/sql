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

```
