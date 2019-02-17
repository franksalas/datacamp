# RDB02 DC LEFT & RIGHT JOINs

# INNER JOIN
![](https://i.imgur.com/UGgppe5.png)

# LEFT JOIN

![](https://i.imgur.com/743I9fT.png)
![](https://i.imgur.com/dzSpHUf.png)
---
![](https://i.imgur.com/WToOGGO.png)


## The Syntax of a LEFT JOIN
```sql
SELECT p1.country, prime_minister, president
FROM prime_ministers AS p1
LEFT JOIN presidents AS p2
ON p1.country = p2.country;
```

![](https://i.imgur.com/uDVRBqi.png)



---

# RIGHT JOIN

![](https://i.imgur.com/eRQB0Pu.png)


```sql
SELECT right_table.id AS R_id,
left_table.val AS L_val,
right_table.val AS R_val
FROM left_table
RIGHT JOIN right_table
ON left_table.id = right_table.id;
```

---
# PRACTICE


### Left Join
Now you'll explore the differences between performing an inner join and a left join using the cities and countries tables.

You'll begin by performing an inner join with the cities table on the left and the countries table on the right. Remember to alias the name of the city field as city and the name of the country field as country.

You will then change the query to a left join. Take note of how many records are in each query here!

```
Fill in the code shown to complete the inner join. Note how many records are in the result of the join in the query result tab.
```

```sql
-- get the city name (and alias it), the country code,
-- the country name (and alias it), the region,
-- and the city proper population
SELECT c1.name AS ___, code, c2.name AS ___,
       region, city_proper_pop
-- specify left table
FROM ___ AS ___
-- specify right table and type of join
INNER JOIN ___ AS ___
-- how should the tables be matched?
ON ___.___ = ___.___
-- sort based on descending country code
ORDER BY code ___;
```

- 230 records
```sql
-- get the city name (and alias it), the country code,
-- the country name (and alias it), the region,
-- and the city proper population
SELECT c1.name AS city, code, c2.name AS country,
       region, city_proper_pop
-- specify left table
FROM cities AS c1
-- specify right table and type of join
INNER JOIN countries AS c2
-- how should the tables be matched?
ON c1.country_code = c2.code
-- sort based on descending country code
ORDER BY code DESC;
```


```
Change the code to perform a LEFT JOIN instead of an INNER JOIN. After executing this query, note how many records the query result contains.
```
- 236 records
```sql
-- get the city name (and alias it), the country code,
-- the country name (and alias it), the region,
-- and the city proper population
SELECT c1.name AS city, code, c2.name AS country,
       region, city_proper_pop
-- specify left table
FROM cities AS c1
-- specify right table and type of join
LEFT JOIN countries AS c2
-- how should the tables be matched?
ON c1.country_code = c2.code
-- sort based on descending country code
ORDER BY code DESC;
```


### Left join (2)
Next, you'll try out another example comparing an inner join to its corresponding left join. Before you begin though, take note of how many records are in both the countries and languages tables below.

You will begin with an inner join on the countries table on the left with the languages table on the right. Then you'll change the code to a left join in the next bullet.

Note the use of multi-line comments here using /* and */.

```
Perform an inner join. Alias the name of the country field as country and the name of the language field as language. Sort based on descending country name.
```

```sql
/*
select country name AS country, the country's local name,
the language name AS language, and
the percent of the language spoken in the country
*/
```
```sql
___ c.name AS country, local_name, l.name AS language, percent
-- countries on the left (alias as c)
FROM ___ AS ___
-- appropriate join with languages (as l) on the right
___ JOIN ___ AS ___
-- give fields to match on
ON ___.___ = ___.___
-- sort by descending country name
ORDER BY country ___;
```

- `INNER JOIN`: 914 rows
```sql
/*
select country name AS country, the country's local name,
the language name AS language, and
the percent of the language spoken in the country
*/
SELECT c.name AS country, local_name, l.name AS language, percent
-- countries on the left (alias as c)
FROM countries AS c
-- appropriate join with languages (as l) on the right
INNER JOIN languages AS l
-- give fields to match on
ON c.code = l.code
```
```
Perform a left join instead of an inner join. Observe the result, and also note the change in the number of records in the result. Carefully review which records appear in the left join result, but not in the inner join result.
```

- `LEFT JOIN`: 921 rows
```sql
/*
select country name AS country, the country's local name,
the language name AS language, and
the percent of the language spoken in the country
*/
SELECT c.name AS country, local_name, l.name AS language, percent
-- countries on the left (alias as c)
FROM countries AS c
-- appropriate join with languages (as l) on the right
LEFT JOIN languages AS l
-- give fields to match on
ON c.code = l.code
```

### Left join (3)
You'll now revisit the use of the AVG() function introduced in our Intro to SQL for Data Science course. You will use it in combination with left join to determine the average gross domestic product (GDP) per capita by region in 2010.

```
Begin with a left join with the countries table on the left and the economies table on the right.
Focus only on records with 2010 as the year.
```

```sql
-- select name, region, and gdp_percapita
SELECT ___, ___, ___
-- from countries (alias c) on the left
FROM ___ AS ___
-- left join with economies (alias e)
LEFT JOIN ___ AS ___
-- match on code fields
ON ___.___ = ___.___
-- focus on 2010 entries
WHERE ___ = ___;
```

```sql
-- select name, region, and gdp_percapita
SELECT name, region, gdp_percapita
-- from countries (alias c) on the left
FROM countries AS c
-- left join with economies (alias e)
LEFT JOIN economies AS e
-- match on code fields
ON c.code = e.code
-- focus on 2010 entries
WHERE year = 2010;
```

```
Modify your code to calculate the average GDP per capita AS avg_gdp for each region in 2010. Select the region and avg_gdp fields.
```

```sql
-- Select region, average gdp_percapita (alias avg_gdp)
SELECT ___
-- From countries (alias c) on the left
FROM ___ AS ___
-- Join with economies (alias e)
LEFT JOIN ___ AS ___
-- Match on code fields
ON ___.___ = ___.___
-- Focus on 2010 
WHERE ___ = ___
-- Group by region
GROUP BY ___;
```

```sql
-- Select region, average gdp_percapita (alias avg_gdp)
SELECT region, AVG(gdp_percapita) AS avg_gdp
-- From countries (alias c) on the left
FROM countries AS c
-- Join with economies (alias e)
LEFT JOIN economies AS e
-- Match on code fields
ON c.code = e.code
-- Focus on 2010 
WHERE year = 2010
-- Group by region
GROUP BY region;
```

```
Arrange this data on average GDP per capita for each region in 2010 from highest to lowest average GDP per capita.
```

```sql
-- Select region, average gdp_percapita (alias avg_gdp)
SELECT ___
-- From countries (alias c) on the left
FROM ___ AS ___
-- Join with economies (alias e)
LEFT JOIN ___ AS ___
-- Match on code fields
ON ___.___ = ___.___
-- Focus on 2010 
WHERE ___ = ___
-- Group by region
GROUP BY ___
-- Order by avg_gdp, descending
ORDER BY ___ ___;
```

```sql
-- Select region, average gdp_percapita (alias avg_gdp)
SELECT region, AVG(gdp_percapita) AS avg_gdp
-- From countries (alias c) on the left
FROM countries AS c
-- Join with economies (alias e)
LEFT JOIN economies AS e
-- Match on code fields
ON c.code = e.code
-- Focus on 2010 
WHERE year = 2010
-- Group by region
GROUP BY region
-- Order by avg_gdp, descending
ORDER BY avg_gdp DESC;
```
### Right join
Right joins aren't as common as left joins. One reason why is that you can always write a right join as a left join.

```
The left join code is commented out here. Your task is to write a new query using rights joins that produces the same result as what the query using left joins produces. Keep this left joins code commented as you write your own query just below it using right joins to solve the problem.

Note the order of the joins matters in your conversion to using right joins!
```

```sql
-- convert this code to use RIGHT JOINs instead of LEFT JOINs
/*
SELECT cities.name AS city, urbanarea_pop, countries.name AS country,
       indep_year, languages.name AS language, percent
FROM cities
LEFT JOIN countries
ON cities.country_code = countries.code
LEFT JOIN languages
ON countries.code = languages.code
ORDER BY city, language;
*/

SELECT cities.name AS city, urbanarea_pop, countries.name AS country,
       indep_year, languages.name AS language, percent
FROM languages
RIGHT JOIN ___
ON ___.___ = ___.___
RIGHT JOIN ___
ON ___.___ = ___.___
ORDER BY city, language;
```

```sql

```

---
# FULL JOINs

## INNER JOIN vs LEFT JOIN

![](https://i.imgur.com/c4D2F0r.png)

## LEFT JOIN vs RIGHT JOIN
![](https://i.imgur.com/7X8qByL.png)


## FULL JOIN

![](https://i.imgur.com/PAb1A9S.png)

![](https://i.imgur.com/uBMc6g9.png)

```sql
SELECT left_table.id AS L_id,
right_table.id AS R_id,
left_table.val AS L_val,
right_table.val AS R_val
FROM left_table
FULL JOIN right_table
USING (id);
```

### FULL JOIN example using leaders database

```sql
SELECT p1.country AS pm_co, p2.country AS pres_co,
prime_minister, president
FROM prime_ministers AS p1
FULL JOIN presidents AS p2
ON p1.country = p2.country;
```
![](https://i.imgur.com/xZqP0Se.png)


# CROSSing the Rubicon

## Pairing prime ministers with presidents

```sql
SELECT prime_minister, president
FROM prime_ministers AS p1
CROSS JOIN presidents AS p2
WHERE p1.continent IN ('North America', 'Oceania');
```

![](https://i.imgur.com/EGfsgAX.png)

---
## PRACTICE