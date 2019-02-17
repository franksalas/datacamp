# RDB01 Joining Data in SQL
# Introduction to joins


![](https://i.imgur.com/sOhEvZT.png)


![](https://i.imgur.com/TSymyEr.png)


![](https://i.imgur.com/uTh5tMg.png)


![](https://i.imgur.com/qxC1XLU.png)

## Example

- Presidents table
```sql
SELECT *
FROM presidents;
```

```
+-----------+---------------+-------------------------+
| country   | continent     | president               |
|-----------+---------------+-------------------------|
| Egypt     | Africa        | Abdel Fattah el-Sisi    |
| Portugal  | Europe        | Marcelo Rebelo de Sousa |
| Haiti     | North America | Jovenel Moise           |
| Uruguay   | South America | Jose Mujica             |
| Liberia   | Africa        | Ellen Johnson Sirleaf   |
| Chile     | South America | Michelle Bachelet       |
| Vietnam   | Asia          | Tran Dai Quang          |
+-----------+---------------+-------------------------+
```

## Inner Join in SQL

```sql
SELECT p1.country, p1.continent, 
       prime_minister, president
FROM prime_ministers AS p1
INNER JOIN presidents AS p2
ON p1.country = p2.country;
```

```
 +-----------+---------------+--------------------+-------------------------+
| country   | continent     | prime_minister     | president               |
|-----------+---------------+--------------------+-------------------------|
| Egypt     | Africa        | Sherif Ismail      | Abdel Fattah el-Sisi    |
| Portugal  | Europe        | Antonio Costa      | Marcelo Rebelo de Sousa |
| Vietnam   | Asia          | Nguyen Xuan Phuc   | Tran Dai Quang          |
| Haiti     | North America | Jack Guy Lafontant | Jovenel Moise           |
+-----------+---------------+--------------------+-------------------------+
```

# Practice

## Inner join
Throughout this course, you'll be working with the countries database containing information about the most populous world cities as well as country-level economic data, population data, and geographic data. This countries database also contains information on languages spoken in each country.

You can see the different tables in this database by clicking on the tabs on the bottom right below query.sql. Click through them to get a sense for the types of data that each table contains before you continue with the course! Take note of the fields that appear to be shared across the tables.

Recall from the video the basic syntax for an `INNER JOIN`, here including all columns in both tables:

```sql
SELECT *
FROM left_table
INNER JOIN right_table
ON left_table.id = right_table.id;
```


You'll start off with a SELECT statement and then build up to an inner join with the cities and countries tables. Let's get to it!

- Begin by selecting all columns from the cities table.
```sql
SELECT *
FROM cities
```


- Inner join the cities table on the left to the countries table on the right, keeping all of the fields in both tables. You should join on the country_code field in cities and the code field in countries. Do not alias your tables here or in the next task though. Using cities and countries is fine for now.
```sql
SELECT *
FROM cities
INNER JOIN countries
ON cities.country_code = countries.code
```





- Modify the SELECT statement to keep only the name of the city, the name of the country, and the name of the region the country resides in.

- Recall from our Intro to SQL for Data Science course that you can alias fields using AS. Alias the name of the city AS city and the name of the country AS country
```sql
SELECT 
    cities.name as city,
    countries.name as country,
    countries.region
FROM 
    cities
INNER JOIN
    countries
ON
    cities.country_code = countries.code
```

## Inner join (2)
Instead of writing the full table name, you can use table aliasing as a shortcut. For tables you also use AS to add the alias immediately after the table name with a space. Check out the aliasing of cities and countries below.



```sql
SELECT c1.name AS city, c2.name AS country
FROM cities AS c1
INNER JOIN countries AS c2
ON c1.country_code = c2.code;
```

Notice that to select a field in your query that appears in multiple tables, you'll need to identify which table/table alias you're referring to by using a . in your SELECT statement.

You'll now explore a way to get data from both the countries and economies tables to examine the inflation rate for both 2010 and 2015.



- Join the tables countries (left) and economies (right). What field do you need to use in ON to match the two tables?
- Alias countries AS c and economies AS e.
From this join, SELECT:
    - c.code, aliased as country_code.
    - name, year, and inflation_rate, not aliased. 
```sql
SELECT c.code AS country_code, c.name, e.year, e.inflation_rate
FROM countries AS c
INNER JOIN economies AS e
ON c.code = e.code;
```


## Inner join (3)
The ability to combine multiple joins in a single query is a powerful feature of SQL, e.g:


 
```sql
SELECT *
FROM left_table
INNER JOIN right_table
ON left_table.id = right_table.id
INNER JOIN another_table
ON left_table.id = another_table.id;
```
As you can see here it becomes tedious to continually write long table names in joins. This is when it becomes useful to alias each table using the first letter of its name (e.g. countries AS c)! It is standard practice to alias in this way and, if you choose to alias tables or are asked to specifically for an exercise in this course, you should follow this protocol.

Now, for each country, you want to get the country name, its region, and the fertility rate and unemployment rate for both 2010 and 2015.



- Inner join countries (left) and populations (right) on the code and country_code fields respectively.
- Alias countries AS c and populations AS p.
- Select code, name, and region from countries and also select year and fertility_rate from populations (5 fields in total). 
```sql
SELECT c.code, c.name, c.region, p.year, p.fertility_rate
FROM countries AS c
INNER JOIN populations AS p
ON c.code = p.country_code
;
```

- Add an additional inner join with economies to your previous query by joining on code.
- Include the unemployment_rate column that became available through joining with economies.
- Note that year appears in both populations and economies, so you have to explicitly use e.year instead of year as you did before
```sql
SELECT c.code, name, region, p.year, p.fertility_rate, e.year, e.unemployment_rate
FROM countries AS c
INNER JOIN populations AS p
ON c.code = p.country_code
INNER JOIN economies AS e
ON c.code = e.code ;
```

---

# INNER JOIN via USING

![](https://i.imgur.com/vc9uydV.png)


- Inner Join
```sql
SELECT left_table.id AS L_id,
left_table.val AS L_val,
right_table.val AS R_val
FROM left_table
INNER JOIN right_table
ON left_table.id = right_table.id;
```
- Inner Join with USING
```sql
SELECT left_table.id AS L_id,
left_table.val AS L_val,
right_table.val AS R_val
FROM left_table
INNER JOIN right_table
USING (id);
```


### Countries with prime ministers and presidents - again

```sql
SELECT p1.country, p1.continent, prime_minister, president
FROM ___ AS p1
INNER JOIN ___ AS p2
___ (___);
```


- answer
```sql
SELECT p1.country, p1.continent, prime_minister, president
FROM presidents AS p1
INNER JOIN prime_ministers AS p2
USING (country);
```

```
+-----------+---------------+--------------------+-------------------------+
| country   | continent     | prime_minister     | president               |
|-----------+---------------+--------------------+-------------------------|
| Egypt     | Africa        | Sherif Ismail      | Abdel Fattah el-Sisi    |
| Portugal  | Europe        | Antonio Costa      | Marcelo Rebelo de Sousa |
| Vietnam   | Asia          | Nguyen Xuan Phuc   | Tran Dai Quang          |
| Haiti     | North America | Jack Guy Lafontant | Jovenel Moise           |
+-----------+---------------+--------------------+-------------------------+
```


### Notes
We are replacing

```sql
...
INNER JOIN right_table
ON left_table.id = right_table.id;
```
with

```sql
INNER JOIN right_table
USING (id);
```



## Practice


Inner join with using
When joining tables with a common field name, e.g.

```sql
SELECT *
FROM countries
INNER JOIN economies
ON countries.code = economies.code
```
You can use USING as a shortcut:
```sql
SELECT *
FROM countries
INNER JOIN economies
USING(code)

```
You'll now explore how this can be done with the countries and languages tables.




```
Inner join countries on the left and languages on the right with USING(code). Select the fields corresponding to:

country name AS country,
continent name,
language name AS language, and
whether or not the language is official.
Remember to alias your tables using the first letter of their names.
```


```sql
SELECT c.name AS country, c.continent, l.name AS language, l.official
FROM countries AS c
INNER JOIN languages AS l
USING (code);
```


---

# Self-ish joins, just in CASE

- A self join are inner joins where a table joints itself
- they are used to comapre values in a field to other values of the same field from withing the same table.
- 


## Join a table to itself?

### Prime minister table
```
+-----------+---------------+-------------------------+
| country   | continent     | prime_minister          |
|-----------+---------------+-------------------------|
| Egypt     | Africa        | Sherif Ismail           |
| Portugal  | Europe        | Antonio Costa           |
| Vietnam   | Asia          | Nguyen Xuan Phuc        |
| Haiti     | North America | Jack Guy Lafontant      |
| India     | Asia          | Narendra Modi           |
| Australia | Oceania       | Malcolm Turnbull        |
| Norway    | Europe        | Erna Solberg            |
| Brunei    | Asia          | Hassanal Bolkiah        |
| Oman      | Asia          | Qaboos bin Said al Said |
| Spain     | Europe        | Mariano Rajoy           |
+-----------+---------------+-------------------------+
```
### QUESTION
Wha tif you wanted to create a new table showing countries that are in the same continent matched as pairs?

## Join prime_ministers to itself?
```sql
SELECT p1.country AS country1, p2.country AS country2, p1.continent
FROM prime_ministers AS p1
INNER JOIN prime_ministers AS p2
ON p1.continent = p2.continent
LIMIT 14;
```
- Result
```

+------------+------------+---------------+
| country1   | country2   | continent     |
|------------+------------+---------------|
| Egypt      | Egypt      | Africa        |
| Portugal   | Spain      | Europe        |
| Portugal   | Norway     | Europe        |
| Portugal   | Portugal   | Europe        |
| Vietnam    | Oman       | Asia          |
| Vietnam    | Brunei     | Asia          |
| Vietnam    | India      | Asia          |
| Vietnam    | Vietnam    | Asia          |
| Haiti      | Haiti      | North America |
| India      | Oman       | Asia          |
| India      | Brunei     | Asia          |
| India      | India      | Asia          |
| India      | Vietnam    | Asia          |
| Australia  | Australia  | Oceania       |
+------------+------------+---------------+
```
#### Problem
- The result is pairng each coutnry with every other coutnry in its same continent
- we don twant to list the country with itself after all
- we dont want to include rows where the coutnry is the same in the `country1` and `country2` fields
- 



## Finishing off the self-join on prime_ministers
```sql
SELECT p1.country AS country1, p2.country AS country2, p1.continent
FROM prime_ministers AS p1
INNER JOIN prime_ministers AS p2
ON p1.continent = p2.continent AND p1.country <> p2.country
LIMIT 13;
```
- solution
- here the `AND` clause checks tha tmultiple conditions are met
- here a match will not be made between `prime_ministers` and itself if the countries match

```
+------------+------------+-------------+
| country1   | country2   | continent   |
|------------+------------+-------------|
| Portugal   | Spain      | Europe      |
| Portugal   | Norway     | Europe      |
| Vietnam    | Oman       | Asia        |
| Vietnam    | Brunei     | Asia        |
| Vietnam    | India      | Asia        |
| India      | Oman       | Asia        |
| India      | Brunei     | Asia        |
| India      | Vietnam    | Asia        |
| Norway     | Spain      | Europe      |
| Norway     | Portugal   | Europe      |
| Brunei     | Oman       | Asia        |
| Brunei     | India      | Asia        |
| Brunei     | Vietnam    | Asia        |
+------------+------------+-------------+
```



## CASE WHEN and THEN

```
+-----------+---------------+--------------+
| name      | continent     |   indep_year |
|-----------+---------------+--------------|
| Australia | Oceania       |         1901 |
| Brunei    | Asia          |         1984 |
| Chile     | South America |         1810 |
| Egypt     | Africa        |         1922 |
| Haiti     | North America |         1804 |
| India     | Asia          |         1947 |
| Liberia   | Africa        |         1847 |
| Norway    | Europe        |         1905 |
| Oman      | Asia          |         1951 |
| Portugal  | Europe        |         1143 |
| Spain     | Europe        |         1492 |
| Uruguay   | South America |         1828 |
| Vietnam   | Asia          |         1945 |
+-----------+---------------+--------------+
```

## QUESTION
Suppose we want to group `indep_year` into categories
- before 1900
- between 1900 and 1930
- after 1900

## Preparing `indep_year_group` in states
```sql
SELECT name, continent, indep_year,
    CASE WHEN ___ < ___  THEN 'before 1900'
        WHEN indep_year <= 1930 THEN '___'
        ELSE '___' END 
        AS indep_year_group
FROM states
ORDER BY indep_year_group;
```

## Creating `indep_year_group` in states

```sql
SELECT name, continent, indep_year,
    CASE WHEN indep_year < 1900 THEN 'before 1900'
         WHEN indep_year <= 1930 THEN 'between 1900 and 1930'
         ELSE 'after 1930' END
         AS indep_year_group
FROM states
ORDER BY indep_year_group;
```


```sql
+-----------+---------------+--------------+-----------------------+
| name      | continent     |   indep_year | indep_year_group      |
|-----------+---------------+--------------+-----------------------|
| Brunei    | Asia          |         1984 | after 1930            |
| India     | Asia          |         1947 | after 1930            |
| Oman      | Asia          |         1951 | after 1930            |
| Vietnam   | Asia          |         1945 | after 1930            |
| Liberia   | Africa        |         1847 | before 1900           |
| Chile     | South America |         1810 | before 1900           |
| Haiti     | North America |         1804 | before 1900           |
| Portugal  | Europe        |         1143 | before 1900           |
| Spain     | Europe        |         1492 | before 1900           |
| Uruguay   | South America |         1828 | before 1900           |
| Norway    | Europe        |         1905 | between 1900 and 1930 |
| Australia | Oceania       |         1901 | between 1900 and 1930 |
| Egypt     | Africa        |         1922 | between 1900 and 1930 |
+-----------+---------------+--------------+-----------------------+
```
---
# Practice


## Self-join
In this exercise, you'll use the populations table to perform a self-join to calculate the percentage increase in population from 2010 to 2015 for each country code!

Since you'll be joining the populations table to itself, you can alias populations as p1 and also populations as p2. This is good practice whenever you are aliasing and your tables have the same first letter. Note that you are required to alias the tables with self-joins.


```
Join populations with itself ON country_code.
Select the country_code from p1.
Select the size field from both p1 and p2. SQL won't allow same-named fields, so alias p1.size as size2010 and p2.size as size2015.
```
```sql
SELECT ___.___, 
       ___.___ AS ___,
       ___.___ AS ___
FROM ___ AS ___
___ JOIN ___ AS ___
ON  ___.___ = ___.___;
```

- 
```sql
SELECT p1.country_code, 
       p1.size AS size2010,
       p2.size AS size2015
FROM populations AS p1
INNER JOIN populations AS p2
ON  p1.country_code = p2.country_code;
```

```
Notice from the result that for each country_code you have four entries laying out all combinations of 2010 and 2015.

Extend the ON in your query to include only those records where the p1.year (2010) matches with p2.year - 5 (2015 - 5 = 2010).

This will omit the three entries per country_code that you aren't interested in.
```
```sql
SELECT ___.___,
       ___.___ AS ___,
       ___.___ AS ___
FROM ___ AS ___
INNER JOIN ___ AS ___
ON ___.___ = ___.___
    AND ___.___ = ___.___ - ___;
```

```sql
SELECT p1.country_code,
       p1.size AS size2010,
       p2.size AS size2015
FROM populations AS p1
INNER JOIN populations AS p2
ON p1.country_code = p2.country_code
    AND p1.year = p2.year - 5;
```


```
As you just saw, you can also use SQL to calculate values like p2.year - 5 for you. With two fields like size2010 and size2015, you may want to determine the percentage increase from one field to the next:

With two numeric fields A and B, the percentage growth from A to B can be calculated as (B−A)/A∗100.0.

To SELECT add a new field aliased as growth_perc that calculates the percentage population growth from 2010 to 2015 for each country, using p2.size and p1.size.
```


```sql
SELECT ___.___,
       ___.___ AS ___, 
       ___.___ AS ___,
       ((___.___ - ___.___)/___.___ * 100.0) AS ___
FROM ___ AS ___
INNER JOIN ___ AS ___
ON ___.___ = ___.___
    AND ___.___ = ___.___ - ___;
```


```sql
SELECT p1.country_code,
       p1.size AS size2010,
       p2.size AS size2015,
       ((p2.size - p1.size)/p1.size * 100.0) AS growth_perc
FROM populations AS p1
INNER JOIN populations AS p2
ON p1.country_code = p2.country_code
    AND p1.year = p2.year - 5;
```


### Case when and then
Often it's useful to look at a numerical field not as raw data, but instead as being in different categories or groups.

You can use CASE with WHEN, THEN, ELSE, and END to define a new grouping field.

 
```sql
Using the countries table, create a new field AS geosize_group that groups the countries into three groups:

If surface_area is greater than 2 million, geosize_group is 'large'.
If surface_area is greater than 350 thousand but not larger than 2 million, geosize_group is 'medium'.
Otherwise, geosize_group is 'small'.
```

```sql
SELECT name, continent, code, surface_area,
        -- first case
    CASE WHEN ___ > ___ THEN '___'
        -- second case
        WHEN > ___ THEN ___
        -- else clause + end
        ELSE ___ END
        AS ___
FROM ___;
```

```sql
SELECT name, continent, code, surface_area,
        -- first case
    CASE WHEN surface_area > 2000000 THEN 'large'
        -- second case
        WHEN surface_area > 350000 THEN 'medium'
        -- else clause + end
        ELSE 'small' END
        AS geosize_group
FROM countries;
```


## Inner challenge
The table you created with the added geosize_group field has been loaded for you here with the name countries_plus. Observe the use of (and the placement of) the INTO command to create this countries_plus table:

```sql
SELECT name, continent, code, surface_area,
    CASE WHEN surface_area > 2000000
            THEN 'large'
       WHEN surface_area > 350000
            THEN 'medium'
       ELSE 'small' END
       AS geosize_group
INTO countries_plus
FROM countries;
```


You will now explore the relationship between the size of a country in terms of surface area and in terms of population using grouping fields created with CASE.

By the end of this exercise, you'll be writing two queries back-to-back in a single script. You got this!


 
```sql
Using the populations table focused only for the year 2015, create a new field AS popsize_group to organize population size into

'large' (> 50 million),
'medium' (> 1 million), and
'small' groups.
Select only the country code, population size, and this new popsize_group as fields.
```


```sql
SELECT country_code, size,
    CASE WHEN ___ > ___ THEN ___
        WHEN ___ > ___ THEN ___
        ELSE ___ END
        AS popsize_group
FROM ___
WHERE ___ = ___;
```

```sql
SELECT country_code, size,
    CASE WHEN size > 50000000 THEN 'large'
        WHEN size > 1000000 THEN 'medium'
        ELSE 'small' END
        AS popsize_group
FROM populations
WHERE year = 2015;
```


```
Use INTO to save the result of the previous query as pop_plus. You can see an example of this in the countries_plus code in the assignment text. Make sure to include a ; at the end of your WHERE clause!

Then, include another query below your first query to display all the records in pop_plus using SELECT * FROM pop_plus; so that you generate results and this will display pop_plus in query 
```

- 
```sql
-- first query
SELECT country_code, size,
    CASE WHEN size > 50000000 THEN 'large'
        WHEN size > 1000000 THEN 'medium'
        ELSE 'small' END
        AS popsize_group
INTO pop_plus
FROM populations
WHERE year = 2015;
-- second query
SELECT *
FROM pop_plus;
```


```sql
- Keep the first query intact that creates pop_plus using INTO.
- Remove the SELECT * FROM pop_plus; code and instead write a second query to join countries_plus AS c on the left with pop_plus AS p on the right matching on the country code fields.
- Select the name, continent, geosize_group, and popsize_group fields.
- Sort the data based on geosize_group, in ascending order so that large appears on top.
```

```sql
SELECT country_code, size,
    CASE WHEN size > 50000000 THEN 'large'
        WHEN size > 1000000 THEN 'medium'
        ELSE 'small' END
        AS popsize_group
INTO pop_plus
FROM populations
WHERE year = 2015;

SELECT name, continent, geosize_group, popsize_group
FROM countries_plus AS c
INNER JOIN pop_plus AS p
ON c.code = p.country_code
ORDER BY geosize_group;

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```


- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```


- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```


- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```


- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```


- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```


- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```


- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```


- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```


- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```

- 
```sql

```