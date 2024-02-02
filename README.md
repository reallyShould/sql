# sql
## 0
```sql
SELECT name, rating FROM pizzeria
LEFT JOIN person_visits
	ON pizzeria.id = person_visits.pizzeria_id
WHERE person_visits.pizzeria_id is null
```
![image](https://github.com/reallyShould/sql/assets/77869589/cb5ee537-04b3-4327-a04d-784d1436ebfd)

## 1
```sql
SELECT DISTINCT visit_date FROM person_visits pv
LEFT JOIN (SELECT missing_date::date FROM generate_series('2022-01-1', '2022-01-10', interval '1 day')
	as missing_date
	JOIN person_visits pv
		ON pv.visit_date = missing_date
	WHERE pv.person_id = 1 OR pv.person_id = 2
)
as md
ON visit_date = md.missing_date
WHERE missing_date IS null
```
![image](https://github.com/reallyShould/sql/assets/77869589/e0850dcf-cd38-4cf4-89e1-9aef5d547b4e)

## 2
```sql
SELECT COALESCE (person.name, '-'), i.visit_date, COALESCE (pizzeria.name, '-') FROM (
	SELECT person_id, visit_date, pizzeria_id FROM person_visits
	WHERE visit_date BETWEEN '2022-01-01' and '2022-01-03'
	) as i
FULL JOIN person
	ON person.id = i.person_id
FULL JOIN pizzeria
	ON pizzeria.id = i.pizzeria_id
ORDER BY 1, 2, 3
```
![image](https://github.com/reallyShould/sql/assets/77869589/424fbae2-747d-448a-8ee4-a9f445b51db2)

## 3
```sql
Надо будет сделать, а пока шиш
```

## 4
```sql
SELECT pizza_name, pizzeria.name as pizzeria_name, price FROM menu
JOIN pizzeria
	ON pizzeria.id = menu.pizzeria_id
WHERE pizza_name = 'mushroom pizza' or pizza_name = 'pepperoni pizza'
ORDER BY 1, 2
```
![image](https://github.com/reallyShould/sql/assets/77869589/021358af-7770-4935-ad55-6a40ef5ddd63)

## 5
```sql
SELECT name FROM person
WHERE person.age > 25 and person.gender = 'female'
ORDER BY 1
```
![image](https://github.com/reallyShould/sql/assets/77869589/92647251-52db-492e-886b-a4f72c88a3c7)

## 6
```sql
SELECT menu.pizza_name, pizzeria.name as pizzeria_name FROM person_order
FULL JOIN person
	ON person.id = person_order.person_id
FULL JOIN menu
	ON menu.id = person_order.menu_id
FULL JOIN pizzeria
	ON pizzeria.id = menu.pizzeria_id
WHERE person.name = 'Denis' or person.name = 'Anna'
ORDER BY 1, 2

```
![image](https://github.com/reallyShould/sql/assets/77869589/350d3458-598a-4d25-bfc1-44109ee91823)

## 7
```sql
SELECT pizzeria.name as pizzeria FROM person_visits
FULL JOIN pizzeria
	ON pizzeria.id = person_visits.pizzeria_id
FULL JOIN person
	ON person.id = person_visits.person_id
FULL JOIN person_order
	ON person_order.order_date = person_visits.visit_date
FULL JOIN menu
	ON menu.id = person_order.menu_id
WHERE visit_date = '2022-01-8' and menu.price <= 800 and person.name = 'Dmitriy'
```
![image](https://github.com/reallyShould/sql/assets/77869589/e28a9f74-bd7c-4ff6-ae01-d0225c4258be)

## 8
```sql
SELECT p.name FROM person_order po
JOIN menu m
	ON m.id = po.menu_id
JOIN person p
	ON p.id = po.person_id
WHERE p.gender = 'male'
	and (pizza_name = 'pepperoni pizza' or pizza_name = 'mushroom pizza') 
	and (p.address = 'Moscow' or p.address = 'Samara')
ORDER BY 1 DESC
```
![image](https://github.com/reallyShould/sql/assets/77869589/805267f4-d9c9-4133-a9ac-8565de780fe0)

## 9
```sql
SELECT tab.person_name FROM (
	SELECT p.id as person_id, m.id as menu_id, m.pizza_name as pizza, p.name person_name FROM person_order po
	JOIN menu m
		ON m.id = po.menu_id
	JOIN person p
		ON p.id = po.person_id
	
	WHERE p.gender = 'female'
		and (pizza_name = 'pepperoni pizza') 
) as tab
JOIN (
	SELECT p.id as person_id, m.id as menu_id, m.pizza_name as pizza, p.name person_name FROM person_order po
	JOIN menu m
		ON m.id = po.menu_id
	JOIN person p
		ON p.id = po.person_id
	
	WHERE p.gender = 'female'
		and (pizza_name = 'cheese pizza') 
) as tab2
	ON tab2.person_id = tab.person_id

```
![image](https://github.com/reallyShould/sql/assets/77869589/f5cc8e58-ee32-4036-b2a7-862056ab7b2c)

## 10
```sql
SELECT p1.name as person_name1, p2.name as person_name2, p1.address as common_address FROM person p1
JOIN person p2 
	ON p1.address = p2.address
WHERE p2.name > p1.name
ORDER BY 1, 2, 3;
```
![image](https://github.com/reallyShould/sql/assets/77869589/adf2a4c3-69f0-4855-aebc-27457cc696e1)
