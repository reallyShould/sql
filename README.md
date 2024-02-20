# sql
## 0
```sql
CREATE TABLE person_discounts ( 
	id BIGINT PRIMARY KEY,
	person_id BIGINT NOT NULL,
	pizzeria_id BIGINT NOT NULL,
	discout FLOAT DEFAULT NULL,
	CONSTRAINT fk_person_discounts_person_id FOREIGN KEY (person_id) REFERENCES person(id),
	CONSTRAINT fk_person_discounts_pizzeria_id FOREIGN KEY (pizzeria_id) REFERENCES pizzeria(id)
  );
SELECT * FROM person_discounts;
```
![image](https://github.com/reallyShould/sql/assets/77869589/74e9d8e3-9eff-4a17-800b-b20e5a38764a)

## 1
```sql
INSERT INTO person_discounts 
	SELECT
		ROW_NUMBER() OVER(ORDER BY 1) as id,
		person_id,
		pizzeria_id,
		CASE
			WHEN count = 1 THEN 10.5
			WHEN count = 2 THEN 22
			ELSE 30
		END
	FROM (
		 SELECT po.person_id, m.pizzeria_id, COUNT(*)
		 FROM person_order po
		 JOIN menu m ON m.id = po.menu_id
		 GROUP BY 1, 2
		 ORDER BY 1, 2
		 );
SELECT * FROM person_discounts 
```
![image](https://github.com/reallyShould/sql/assets/77869589/a73179bf-d398-4a3f-8c35-4e6da853934d)

## 2
```sql
SELECT 
	p.name,
	m.pizza_name, 
	m.price, 
	m.price - (m.price / 100 * pd.discout) as discount_price, 
	pz.name
FROM person_order po
JOIN person_discounts pd ON pd.person_id = po.person_id
JOIN person p ON p.id = pd.person_id
JOIN pizzeria pz ON pz.id = pd.pizzeria_id
JOIN menu m ON m.id = po.menu_id
ORDER BY 1, 2

```
![image](https://github.com/reallyShould/sql/assets/77869589/ef9925fa-4a3a-4cd4-bf56-5f0f4a9638d9)

## 3
```sql

```

## 4
```sql
ALTER TABLE person_discounts
	ADD CONSTRAINT ch_nn_person_id CHECK (person_id IS NOT NULL);
	
ALTER TABLE person_discounts
	ADD CONSTRAINT ch_nn_pizzeria_id CHECK (pizzeria_id IS NOT NULL);
	
ALTER TABLE person_discounts
	ADD CONSTRAINT ch_nn_discount CHECK (discout IS NOT NULL);
	
ALTER TABLE person_discounts
	ALTER discout SET DEFAULT 0;
	
ALTER TABLE person_discounts
	ADD CONSTRAINT ch_range_discount CHECK (discout BETWEEN 0 AND 100);
```
![image](https://github.com/reallyShould/sql/assets/77869589/a5afb37e-4982-4284-b871-d77a949de622)

## 5
```sql
COMMENT ON TABLE person_discounts IS 'Table with discounts';
COMMENT ON COLUMN person_discounts.id IS 'Discount id';
COMMENT ON COLUMN person_discounts.person_id IS 'Person id';
COMMENT ON COLUMN person_discounts.pizzeria_id IS 'Pizzeria id';
COMMENT ON COLUMN person_discounts.discout IS 'Discount';
```
![image](https://github.com/reallyShould/sql/assets/77869589/223fa618-f75a-4b77-9c8b-cd43d974a019)

## 6 
```sql

```
