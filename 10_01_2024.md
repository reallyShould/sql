# sql
## 1
```sql
SELECT object_name FROM (
	SELECT name as object_name, 'person' as type FROM person
	union all
	SELECT pizza_name, 'pizza' from menu
	order by type, object_name
) as type;
```
![image](https://github.com/reallyShould/sql/assets/77869589/353d2b33-ff29-477f-b578-4a80c9dd78dc)

## 2
```sql
SELECT pizza_name FROM menu 
INTERSECT
SELECT pizza_name FROM menu
ORDER BY pizza_name DESC
```
![image](https://github.com/reallyShould/sql/assets/77869589/350fc611-0e53-4715-8c1a-07939a3be66f)

## 3
```sql
SELECT order_date as action_date, person_id FROM person_order
INTERSECT all
Select visit_date, person_id FROM person_visits
ORDER BY action_date, person_id desc;
```
![image](https://github.com/reallyShould/sql/assets/77869589/0b0638c6-317a-4031-b28d-b62ddb597743)

## 4
```sql
SELECT person_id, order_date FROM person_order
WHERE order_date = '07-01-2022'
INTERSECT 
SELECT person_id, visit_date FROM person_visits
```
![image](https://github.com/reallyShould/sql/assets/77869589/a97157a4-d657-4f29-a5ee-30d9b9335c3d)

## 5
```sql
SELECT 
	person.id as "person.id",
	person.name as "person.name",
	person.age, person.gender,
	person.address,
	pizzeria.id as "pizzeria.id",
	pizzeria.name as "pizzeria.name",
	rating 
from person, pizzeria 
ORDER BY person.id, pizzeria.id
```
![image](https://github.com/reallyShould/sql/assets/77869589/ec8c9341-0b50-414e-840d-e4a9fae2cce4)

## 6
```sql
SELECT action_date, person.name FROM(
	SELECT order_date as action_date, person_id FROM person_order
	INTERSECT all
	Select visit_date, person_id FROM person_visits
	ORDER BY action_date, person_id desc
) as foo
JOIN person on foo.person_id=person.id 
```
![image](https://github.com/reallyShould/sql/assets/77869589/12d178ea-3eac-46be-957d-54eddf5d3e90)

## 7
```sql
SELECT order_date, person.name || ' (age:' || person.age || ')' as person_information FROM person_order
JOIN person on person_order.person_id=person.id
ORDER by person_information
```
![image](https://github.com/reallyShould/sql/assets/77869589/acb2a096-8b5b-481f-b231-31b70b21043f)

## 8
```sql
SELECT order_date, person.name || ' (age:' || person.age || ')' as person_information FROM
	(SELECT order_date, person_id FROM person_order) as s
NATURAL JOIN person
```
![image](https://github.com/reallyShould/sql/assets/77869589/d7fa1861-29c2-4791-850b-fe5f5f4f0647)

## 9 
