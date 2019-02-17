# RDB03 State of the UNION

## Set Theory Venn Diagrams
![](https://i.imgur.com/rYBr6ND.png)



### UNION
![](https://i.imgur.com/ImKKToE.png)


### UNION ALL
![](https://i.imgur.com/YMoPlAA.png)

### monarchs table

```sql
SELECT *
FROM monarchs;
```

![](https://i.imgur.com/YdmDqiz.png)


## All prime ministers and monarchs

```sql
SELECT prime_minister AS leader, country
FROM prime_ministers
UNION
SELECT monarch, country
FROM monarchs
ORDER BY country;
```

### Resulting table from UNION
![](https://i.imgur.com/mUDC4T8.png)



## UNION ALL with leaders

```sql
SELECT prime_minister AS leader, country
FROM prime_ministers
UNION ALL
SELECT monarch, country
FROM monarchs
ORDER BY country
LIMIT 10;
```

![](https://i.imgur.com/Jqjh0dU.png)

---
## PRACTICE



---

# INTERSECTional data science

## INTERSECT diagram and SQL code

```sql
SELECT id
FROM left_one
INTERSECT
SELECT id
FROM right_one;
```
![](https://i.imgur.com/EayNcrG.png)

### Prime minister and president countries

```sql
SELECT country
FROM prime_ministers
INTERSECT
SELECT country
FROM presidents;

```


![](https://i.imgur.com/juXyriF.png)


### INTERSECT on two fields
```sql
SELECT country, prime_minister AS leader
FROM prime_ministers
INTERSECT
SELECT country, president
FROM presidents;
```

```
+-----------+----------+
| country   | leader   |
|-----------+----------|
+-----------+----------+
```
---

## PRACTICE


---

# EXCEPTional


## Monarchs that aren't prime ministers


```sql
SELECT monarch, country
FROM monarchs
EXCEPT
SELECT prime_minister, country
FROM prime_ministers;
```

```
+-----------+-----------+
| monarch   | country   |
|-----------+-----------|
| Harald V  | Norway    |
| Felipe VI | Spain     |
+-----------+-----------+
```

![](https://i.imgur.com/KjwT2p8.png)


---

# PRACTICE


---

# Semi-joins and Anti-joins

## Building up to a semi-join
```sql
SELECT name
FROM states
WHERE indep_year < 1800;
```

```
+----------+
| name     |
|----------|
| Portugal |
| Spain    |
+----------+
```


## Another step towards the semi-join
```sql
SELECT president, country, continent
FROM presidents;
```




![](https://i.imgur.com/nf1ReGv.png)

## Finish the semi-join (an intro to subqueries)
```sql
SELECT president, country, continent
FROM presidents
WHERE country IN
(SELECT name
FROM states
WHERE indep_year < 1800);
```
![](https://i.imgur.com/49lFKLG.png)


## An anti-join
```sql
SELECT president, country, continent
FROM presidents
WHERE ___ LIKE '___'
AND country ___ IN
(SELECT name
FROM states
WHERE indep_year < 1800);
```
```sql
SELECT president, country, continent
FROM presidents
WHERE continent LIKE '%America'
AND country NOT IN
(SELECT name
FROM states
WHERE indep_year < 1800);
```




## The result of the anti-join

![](https://i.imgur.com/Q1y1z86.png)

## Semi-join and anti-join diagrams

![](https://i.imgur.com/Lz6T98Q.png)

---

# P