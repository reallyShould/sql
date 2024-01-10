# sql
## Task 2
```sql
select name, age, address from person;
```
![image](https://github.com/reallyShould/sql/assets/77869589/33bb11b9-6752-45c8-8658-7479da92b031)

## Task 3
```sql
select name, age from person
WHERE gender = 'female'
ORDER BY name
```
![image](https://github.com/reallyShould/sql/assets/77869589/274e6470-9394-491b-9e2b-0ce5ad32a134)

## Task 4
```sql
SELECT name, rating FROM pizzeria
WHERE rating >= 3.5
ORDER BY rating DESC
```
![image](https://github.com/reallyShould/sql/assets/77869589/07584c93-68a1-46b9-b210-78c1dbfaeb20)
```sql
SELECT name, rating FROM pizzeria
WHERE rating BETWEEN 3.5 and 5
ORDER BY rating DESC
```
![image](https://github.com/reallyShould/sql/assets/77869589/c9c78e9c-d41d-4e25-a2ac-e7b58f0509a2)


## Task 5
```sql
SELECT DISTINCT person_id FROM person_visits
WHERE visit_date >= '2022-01-04'
ORDER BY person_id DESC
```
![image](https://github.com/reallyShould/sql/assets/77869589/fba8b67d-cc37-4e6f-9a32-cdb87249c164)

## Task 6
```sql
SELECT id, name FROM person 
WHERE person.id IN(select person_id from person_order WHERE order_date = '2022-01-01' OR order_date = '2022-01-02' OR order_date = '2022-01-03')
```
![image](https://github.com/reallyShould/sql/assets/77869589/4cbb17bf-0088-472b-986a-f75868762eac)

## Task 7
```sql
SELECT true FROM person WHERE name = 'Denis'
```
![image](https://github.com/reallyShould/sql/assets/77869589/337ab57f-d128-4cbc-a20e-b5ba306e8e09)

