# RDB04 Subqueries inside WHERE and SELECT clauses

## Subquery inside WHERE clause set-up
![](https://i.imgur.com/TcY2Nyn.png)


## Average fert_rate
```SQL
SELECT AVG(fert_rate)
FROM states;
```
```
+---------+
| avg     |
|---------|
| 2.28385 |
+---------+
```
## Asian countries below average fert_rate
```sql
SELECT name, fert_rate
FROM states
WHERE continent = 'Asia'
AND fert_rate <
(SELECT AVG(fert_rate)
FROM states);
```
```
+---------+-------------+
| name    | fert_rate   |
|---------+-------------|
| Brunei  | 1.96        |
| Vietnam | 1.7         |
+---------+-------------+
```

## Subqueries inside SELECT clauses - setup

```sql
SELECT DISTINCT continent
FROM prime_ministers;
```
```
+---------------+
| continent     |
|---------------|
| Africa        |
| Asia          |
| Europe        |
| North America |
| Oceania       |
+---------------+
```

## Subquery inside SELECT clause - complete

```sql
SELECT DISTINCT continent,
(SELECT COUNT(*)
FROM states
WHERE prime_ministers.continent = states.continent) AS countries_num
FROM prime_ministers;
```
![](https://i.imgur.com/9b6lIB0.png)

---

# PRACTICE



---

# Subquery inside the FROM clause

## Build-up
```sql
SELECT continent, MAX(women_parli_perc) AS max_perc
FROM states
GROUP BY continent
ORDER BY continent;
```

![](https://i.imgur.com/jOOvdwk.png)

## Focusing on records in monarchs
```sql
SELECT monarchs.continent
FROM monarchs, states
WHERE monarchs.continent = states.continent
ORDER BY continent;
```

![](https://i.imgur.com/aadKCCF.png)


## Finishing off the subquery
```sql
SELECT DISTINCT monarchs.continent, subquery.max_perc
FROM monarchs,
(SELECT continent, MAX(women_parli_perc) AS max_perc
FROM states
GROUP BY continent) AS subquery
WHERE monarchs.continent = subquery.continent
ORDER BY continent;
```
![](https://i.imgur.com/YyUbuXn.png)
.

---
# PRACTICE



---

# COURSE REVIEW

## TYPES OF JOINS
![](https://i.imgur.com/sMHls4G.png)


## INNER JOIN vs LEFT JOIN
![](https://i.imgur.com/Y0HMF1C.png)

## RIGHT JOIN vs FULL JOIN
![](https://i.imgur.com/gW1m3VO.png)


## CROSS JOIN with code

```sql
SELECT table1.id AS id1,
table2.id AS id2
FROM table1
CROSS JOIN table2;
```
![](https://i.imgur.com/MCoeKiX.png)

## Set Theory Clauses

![](https://i.imgur.com/P7mlkVt.png)


## Semi-joins and Anti-joins
![](https://i.imgur.com/T63Dbtf.png)

## Types of basic subqueries
- Subqueries inside WHERE clauses
- Subqueries inside SELECT clauses
- Subqueries inside FROM clauses

