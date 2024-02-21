# sql
## 0
```sql
SELECT 
	p.id as person_id,
	COUNT(*) as count_of_visits
FROM person p
JOIN person_visits pv ON pv.person_id = p.id
GROUP BY p.id
ORDER BY 2 desc, 1;
```
![image](https://github.com/reallyShould/sql/assets/77869589/11d21f4c-70e1-4eef-b92f-645ac5f43927)

## 1
```sql
SELECT 
	p.name as name,
	COUNT(*) as count_of_visits
FROM person p
JOIN person_visits pv ON pv.person_id = p.id
GROUP BY p.id
ORDER BY 2 desc, 1
LIMIT 4
```
![image](https://github.com/reallyShould/sql/assets/77869589/517bebac-eee4-4938-8949-9c92479ef4e9)

## 2
```sql

```

## 3
```sql
SELECT 
	pz.name as name,
	COUNT(pv) as total_count
FROM person_visits pv
JOIN pizzeria pz ON pz.id = pv.pizzeria_id
JOIN person_order po ON po.order_date = pv.visit_date
GROUP BY pz.name
ORDER BY 2 DESC, 1 
```
![image](https://github.com/reallyShould/sql/assets/77869589/4cec4b8d-9fed-4d5b-b1ab-7e51b93f4db5)
