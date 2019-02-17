# relational db notes

## Beginning your SQL journey

Now that you're familiar with the interface, let's get straight into it.

SQL, which stands for Structured Query Language, is a language for interacting with data stored in something called a relational database.

You can think of a relational database as a collection of tables. A table is just a set of rows and columns, like a spreadsheet, which represents exactly one type of entity. For example, a table might represent employees in a company or purchases made, but not both.

Each row, or record, of a table contains information about a single entity. For example, in a table representing employees, each row represents a single person. Each column, or field, of a table contains a single attribute for all rows in the table. For example, in a table representing employees, we might have a column containing first and last names for all employees.

The table of employees might look something like this:

```table
id	name	age	nationality
1	Jessica	22	Ireland
2	Gabriel	48	France
3	Laura	36	USA
```

---
## SELECTing single columns
While SQL can be used to create and modify databases, the focus of this course will be querying databases. A query is a request for data from a database table (or combination of tables). Querying is an essential skill for a data scientist, since the data you need for your analyses will often live in databases.

In SQL, you can select data from a table using a SELECT statement. For example, the following query selects the name column from the people table:

## Exercise
Select the title column from the films table.

```sql
SELECT title
FROM films
```

- Select the release_year column from the films table.

```sql
SELECT release_year
FROM films
```
- Select the name of each person in the people table.

```sql
SELECT name
FROM people
```

# SELECT DISTINCT
Often your results will include many duplicate values. If you want to select all the unique values from a column, you can use the DISTINCT keyword.

This might be useful if, for example, you're interested in knowing which languages are represented in the films table:
 
```sql
SELECT DISTINCT language
FROM films;
```





- Get all the unique countries represented in the films table.
```sql
SELECT DISTINCT  country
FROM films;
```

- Get all the different film certifications from the films table.
```sql
SELECT DISTINCT  certification
FROM films;
```

- Get the different types of film roles from the roles table.
```sql
SELECT DISTINCT  role
FROM roles;
```


# Learning to COUNT
What if you want to count the number of employees in your employees table? The COUNT statement lets you do this by returning the number of rows in one or more columns.

For example, this code gives the number of rows in the people table:

```sql
SELECT COUNT(*)
FROM people;
```

## Practice with COUNT
As you've seen, COUNT(*) tells you how many rows are in a table. However, if you want to count the number of non-missing values in a particular column, you can call COUNT on just that column.

For example, to count the number of birth dates present in the people table:

```sql
SELECT COUNT(birthdate)
FROM people;
```




- Count the number of rows in the people table.
```sql
SELECT COUNT(*)
FROM people;
```


- Count the number of (non-missing) birth dates in the people table.
```sql
SELECT COUNT(birthdate)
FROM people;
```

- Count the number of unique birth dates in the people table.
```sql
SELECT COUNT(DISTINCT birthdate)
FROM people;
```

- Count the number of unique languages in the films table.
```sql
SELECT COUNT(DISTINCT language)
FROM films
```

- Count the number of unique countries in the films table.
```sql
SELECT COUNT(DISTINCT country)
FROM films;
```
---
# 2. Filtering rows

In SQL, the `WHERE` keyword allows you to filter based on both text and numeric values in a table. There are a few different comparison operators you can use:


- `=` equal
- `<>`` not equal
- `<` less than
- `>` greater than
- `<=` less than or equal to
- `>=` greater than or equal to

For example, you can filter text records such as title. The following code returns all films with the title 'Metropolis':

```sql
SELECT title
FROM films
WHERE title = 'Metropolis';
```

## Simple filtering of numeric values
As you learned in the previous exercise, the WHERE clause can also be used to filter numeric records, such as years or ages.

For example, the following query selects all details for films with a budget over ten thousand dollars:

```sql
SELECT *
FROM films
WHERE budget > 10000;
```


- Get all details for all films released in 2016.
```sql
SELECT *
FROM films
WHERE release_year = 2016
```

- Get the number of films released before 2000.
```sql
SELECT COUNT(*)
FROM films
WHERE release_year < 2000
```

- Get the title and release year of films released after 2000.
```sql
SELECT title,release_year
FROM films
WHERE release_year > 2000
```


## Simple filtering of text
Remember, the WHERE clause can also be used to filter text results, such as names or countries.

For example, this query gets the titles of all films which were filmed in China:

```sql
SELECT title
FROM films
WHERE country = 'China';
```

- Get all details for all French language films.
```sql
SELECT *
FROM films
WHERE language = 'French'
```





- Get the name and birth date of the person born on November 11th, 1974. Remember to use ISO date format ('1974-11-11')!
```sql
SELECT name, birthdate
FROM people
WHERE birthdate = '1974-11-11'
```


- Get the number of Hindi language films.
```sql
SELECT COUNT(*)
FROM films
WHERE language = 'Hindi'
```

- Get all details for all films with an R certification.
```sql
SELECT *
FROM films
WHERE certification = 'R'
```

## WHERE AND
Often, you'll want to select data based on multiple conditions. You can build up your WHERE queries by combining multiple conditions with the AND keyword.

For example,

```sql
SELECT title
FROM films
WHERE release_year > 1994
AND release_year < 2000;
```
gives you the titles of films released between 1994 and 2000.

Note that you need to specify the column name separately for every `AND` condition, so the following would be invalid:

```sql
SELECT title
FROM films
WHERE release_year > 1994 AND < 2000;
```
You can add as many `AND` conditions as you need!


- Get the title and release year for all Spanish language films released before 2000
```sql
SELECT title,release_year
FROM films
WHERE language = 'Spanish'
AND release_year < 2000
```





- Get all details for Spanish language films released after 2000.
```sql
SELECT *
FROM films
WHERE language = 'Spanish'
AND release_year > 2000
```


- Get all details for Spanish language films released after 2000, but before 2010.
```sql
SELECT *
FROM films
WHERE language = 'Spanish'
AND release_year > 2000
AND release_year < 2010
```


## WHERE AND OR
What if you want to select rows based on multiple conditions where some but not all of the conditions need to be met? For this, SQL has the OR operator.

For example, the following returns all films released in either 1994 or 2000:

```sql
SELECT title
FROM films
WHERE release_year = 1994
OR release_year = 2000;
```

Note that you need to specify the column for every OR condition, so the following is invalid:

```sql
SELECT title
FROM films
WHERE release_year = 1994 OR 2000;
```

When combining AND and OR, be sure to enclose the individual clauses in parentheses, like so:

```sql
SELECT title
FROM films
WHERE (release_year = 1994 OR release_year = 1995)
AND (certification = 'PG' OR certification = 'R');
```
Otherwise, due to SQL's precedence rules, you may not get the results you're expecting!


## WHERE AND OR (2)
You now know how to select rows that meet some but not all conditions by combining AND and OR.

For example, the following query selects all films that were released in 1994 or 1995 which had a rating of PG or R

```sql
SELECT title
FROM films
WHERE (release_year = 1994 OR release_year = 1995)
AND (certification = 'PG' OR certification = 'R');
```


Now you'll write a query to get the title and release year of films released in the 90s which were in French or Spanish and which took in more than $2M gross.

It looks like a lot, but you can build the query up one step at a time to get comfortable with the underlying concept in each step. Let's go!

- Get the title and release year for films released in the 90s.
```sql
SELECT title, release_year
FROM films
WHERE release_year >= 1990
AND release_year <= 1999
```


- Now, build on your query to filter the records to only include French or Spanish language films.
```sql
SELECT title, release_year
FROM films
WHERE release_year >= 1990
AND release_year <= 1999
AND (language = 'French' OR language = 'Spanish')
```

- Finally, restrict the query to only return films that took in more than $2M gross.
```sql
SELECT title, release_year
FROM films
WHERE release_year >= 1990
AND release_year <= 1999
AND (language = 'French' OR language = 'Spanish')
AND gross > 2000000;
```


## BETWEEN
As you've learned, you can use the following query to get titles of all films released in and between 1994 and 2000

```sql
SELECT title
FROM films
WHERE release_year >= 1994
AND release_year <= 2000;
```

Checking for ranges like this is very common, so in SQL the BETWEEN keyword provides a useful shorthand for filtering values within a specified range. This query is equivalent to the one above:

```sql
SELECT title
FROM films
WHERE release_year
BETWEEN 1994 AND 2000;
```

It's important to remember that BETWEEN is inclusive, meaning the beginning and end values are included in the results!



## BETWEEN (2)
Similar to the `WHERE` clause, the `BETWEEN` clause can be used with multiple `AND` and `OR` operators, so you can build up your queries and make them even more powerful!

For example, suppose we have a table called kids. We can get the names of all `kids` between the ages of 2 and 12 from the United States:


```sql
SELECT name
FROM kids
WHERE age BETWEEN 2 AND 12
AND nationality = 'USA';
```
Take a go at using `BETWEEN` with `AND` on the films data to get the title and release year of all Spanish language films released between 1990 and 2000 (inclusive) with budgets over $100 million. We have broken the problem into smaller steps so that you can build the query as you go along!


- Get the title and release year of all films released between 1990 and 2000 (inclusive)
```sql
SELECT title, release_year
FROM films
WHERE release_year
BETWEEN 1990 AND 2000;
```


- Now, build on your previous query to select only films that have budgets over $100 million.
```sql
SELECT title, release_year
FROM films
WHERE release_year 
BETWEEN 1990 AND 2000
AND budget > 100000000
```

- Now restrict the query to only return Spanish language films.
```sql
SELECT title, release_year
FROM films
WHERE release_year 
BETWEEN 1990 AND 2000
AND budget > 100000000
AND language = 'Spanish'
```

- Finally, modify to your previous query to include all Spanish language or French language films with the same criteria as before. Don't forget your parentheses!
```sql
SELECT title, release_year
FROM films
WHERE release_year 
BETWEEN 1990 AND 2000
AND budget > 100000000
AND (language = 'Spanish' OR language = 'French');
```
## WHERE IN
As you've seen, WHERE is very useful for filtering results. However, if you want to filter based on many conditions, WHERE can get unwieldy. For example:


```sql
SELECT name
FROM kids
WHERE age = 2
OR age = 4
OR age = 6
OR age = 8
OR age = 10;
```
Enter the `IN` operator! The `IN` operator allows you to specify multiple values in a `WHERE` clause, making it easier and quicker to specify multiple OR conditions! Neat, right?

 
```sql
SELECT name
FROM kids
WHERE age IN (2, 4, 6, 8, 10);
```





- Get the title and release year of all films released in 1990 or 2000 that were longer than two hours. Remember, duration is in minutes!
```sql
SELECT title, release_year
FROM films
WHERE release_year IN (1990, 2000)
AND duration >  120
```


- Get the title and language of all films which were in English, Spanish, or French.
```sql
SELECT title, language
FROM films
WHERE language IN('Spanish', 'English', 'French')
```

- Get the title and certification of all films with an NC-17 or R certification.
```sql
SELECT title, certification
FROM films
WHERE certification IN('NC-17','R')
```

## Introduction to NULL and IS NULL
In SQL, `NULL` represents a missing or unknown value. You can check for `NULL` values using the expression `IS NULL`. For example, to count the number of missing birth dates in the people table:



```sql
SELECT COUNT(*)
FROM people
WHERE birthdate IS NULL;
```
As you can see, `IS NULL` is useful when combined with WHERE to figure out what data you're missing.

Sometimes, you'll want to filter out missing values so you only get results which are not `NULL`. To do this, you can use the IS `NOT NULL` operator.

For example, this query gives the names of all people whose birth dates are not missing in the `people` table.
 
```sql
SELECT name
FROM people
WHERE birthdate IS NOT NULL;
```

## NULL and IS NULL
Now that you know what NULL is and what it's used for, it's time for some practice!

- Get the names of people who are still alive, i.e. whose death date is missing.
```sql
SELECT name
FROM people
WHERE deathdate IS NULL;
```




- Get the title of every film which doesn't have a budget associated with it
```sql
SELECT title
FROM films
WHERE budget IS NULL;
```


- Get the number of films which don't have a language associated with them
```sql

```

- Get the number of films which don't have a language associated with them.
```sql
SELECT COUNT(*)
FROM films
WHERE language IS NULL;
```


## LIKE and NOT LIKE
As you've seen, the `WHERE` clause can be used to filter text data. However, so far you've only been able to filter by specifying the exact text you're interested in. In the real world, often you'll want to search for a pattern rather than a specific text string.

In SQL, the `LIKE` operator can be used in a `WHERE` clause to search for a pattern in a column. To accomplish this, you use something called a wildcard as a placeholder for some other values. There are two wildcards you can use with `LIKE`:

The `%` wildcard will match zero, one, or many characters in text. For example, the following query matches companies like 'Data', 'DataC' 'DataCamp', 'DataMind', and so on:


```sql
SELECT name
FROM companies
WHERE name LIKE 'Data%';
```
The `_` wildcard will match a single character. For example, the following query matches companies like 'DataCamp', 'DataComp', and so on:
 
```sql
SELECT name
FROM companies
WHERE name LIKE 'DataC_mp';
```
You can also use the `NOT LIKE` operator to find records that don't match the pattern you specify.


- Get the names of all people whose names begin with 'B'. The pattern you need is 'B%'.
```sql
SELECT name
FROM people
WHERE name LIKE 'B%';
```






- Get the names of people whose names have 'r' as the second letter. The pattern you need is '_r%'.
```sql
SELECT name
FROM people
WHERE name LIKE '_r%';
```

- Get the names of people whose names don't start with A. The pattern you need is 'A%'.
```sql
SELECT name
FROM people
WHERE name NOT LIKE 'A%';
```
---


# Aggregate Functions

Often, you will want to perform some calculation on the data in a database. SQL provides a few functions, called aggregate functions, to help you out with this.

For example,

```sql
SELECT AVG(budget)
FROM films;
```
gives you the average value from the `budget` column of the `film`s table. Similarly, the `MAX` function returns the highest budget:


```sql
SELECT MAX(budget)
FROM films;
```

The `SUM` function returns the result of adding up the numeric values in a column
```sql
SELECT SUM(budget)
FROM films;
```

You can probably guess what the `MIN `function does! Now it's your turn to try out some SQL functions.


- Use the SUM function to get the total duration of all films.
```sql
SELECT SUM(duration)
FROM films;
```

- Get the average duration of all films.
```sql
SELECT AVG(duration)
FROM films;
```

- Get the duration of the shortest film.
```sql
SELECT MIN(duration)
FROM films;
```

- Get the duration of the longest film.
```sql
SELECT MAX(duration)
FROM films;
```

## Aggregate functions practice
Good work. Aggregate functions are important to understand, so let's get some more practice!



- Use the SUM function to get the total amount grossed by all films.
```sql
SELECT SUM(gross)
FROM films;
```


- Get the average amount grossed by all films.
```sql
SELECT AVG(gross)
FROM films;
```

- Get the amount grossed by the worst performing film
```sql
SELECT MIN(gross)
FROM films;
```

- Get the amount grossed by the best performing film
```sql
SELECT MAX(gross)
FROM films;
```

## Combining aggregate functions with WHERE
Aggregate functions can be combined with the `WHERE` clause to gain further insights from your data.

For example, to get the total budget of movies made in the year 2010 or later:



```sql
SELECT SUM(budget)
FROM films
WHERE release_year >= 2010;
```

- Use the SUM function to get the total amount grossed by all films made in the year 2000 or later.
```sql
SELECT SUM(gross)
FROM films
WHERE release_year >= 2000;
```

- Get the average amount grossed by all films whose titles start with the letter 'A'.
```sql
SELECT AVG(gross)
FROM films
WHERE title LIKE 'A%'
```

- Get the amount grossed by the worst performing film in 1994.
```sql
SELECT MIN(gross)
FROM films
WHERE release_year = 1994
```

- Get the amount grossed by the best performing film between 2000 and 2012, inclusive.
```sql
SELECT MAX(gross)
FROM films
WHERE release_year
BETWEEN 2000 AND 2012
```

## A note on arithmetic
In addition to using aggregate functions, you can perform basic arithmetic with symbols like `+, -, *, and /`.

So, for example, this gives a result of `12`:


```sql
SELECT (4 * 3);

```

However, the following gives a result of 1:
```sql
SELECT (4 / 3);
```

What's going on here?

SQL assumes that if you divide an integer by an integer, you want to get an integer back. So be careful when dividing!

If you want more precision when dividing, you can add decimal places to your numbers. For example,

```sql
SELECT (4.0 / 3.0) AS result;
```
gives you the result you would expect: 1.333.

## It's AS simple AS aliasing
You may have noticed in the first exercise of this chapter that the column name of your result was just the name of the function you used. For example


```sql
SELECT MAX(budget)
FROM films;
```

gives you a result with one column, named max. But what if you use two functions like this?
```sql
SELECT MAX(budget), MAX(duration)
FROM films;
```

Well, then you'd have two columns named max, which isn't very useful!

To avoid situations like this, SQL allows you to do something called aliasing. Aliasing simply means you assign a temporary name to something. To alias, you use the AS keyword, which you've already seen earlier in this course.

For example, in the above example we could use aliases to make the result clearer:
```sql
SELECT MAX(budget) AS max_budget,
       MAX(duration) AS max_duration
FROM films;
```

- Get the title and net profit (the amount a film grossed, minus its budget) for all films. Alias the net profit as `net_profit`.
```sql
SELECT title,(gross - budget) as net_profit
FROM films;
```

- Get the title and duration in hours for all films. The duration is in minutes, so you'll need to divide by 60.0 to get the duration in hours. Alias the duration in hours as `duration_hours`.
```sql
SELECT title,duration/60.0 as duration_hours
FROM films;
```

- Get the average duration in hours for all films, aliased as avg_duration_hours
```sql
SELECT AVG(duration)/60.0 as avg_duration_hours
FROM films;
```

## Even more aliasing
Let's practice your newfound aliasing skills some more before moving on!

Recall: SQL assumes that if you divide an integer by an integer, you want to get an integer back.

This means that the following will erroneously result in 400.0:

```sql
SELECT 45 / 10 * 100.0;
```

This is because 45 / 10 evaluates to an integer (4), and not a decimal number like we would expect.

So when you're dividing make sure at least one of your numbers has a decimal place:

```sql
SELECT 45 * 100.0 / 10;
```

The above now gives the correct answer of 450.0 since the numerator (45 * 100.0) of the division is now a decimal!

- Get the percentage of people who are no longer alive. Alias the result as percentage_dead. Remember to use 100.0 and not 100!
```sql
-- get the count(deathdate) and multiply by 100.0
-- then divide by count(*)
SELECT  count(deathdate)* 100.0/ count(*) as percentage_dead
FROM people;
```

- Get the number of years between the newest film and oldest film. Alias the result as difference.
```sql
SELECT (MAX(release_year) -MIN(release_year)) as difference
FROM films;
```

- Get the number of decades the films table covers. Alias the result as number_of_decades. The top half of your fraction should be enclosed in parentheses.
```sql
SELECT (MAX(release_year)-MIN(release_year))/10
as number_of_decades
FROM films
```
---
# 4. Sorting, grouping and joins

## ORDER BY
Congratulations on making it this far! You now know how to select and filter your results.

In this chapter you'll learn how to sort and group your results to gain further insight. Let's go!

In SQL, the ORDER BY keyword is used to sort results in ascending or descending order according to the values of one or more columns.

By default ORDER BY will sort in ascending order. If you want to sort the results in descending order, you can use the DESC keyword. For example


```sql
SELECT title
FROM films
ORDER BY release_year DESC;
```
gives you the titles of films sorted by release year, from newest to oldest.

## Sorting single columns
Now that you understand how ORDER BY works, give these exercises a go!

- Get the names of people from the people table, sorted alphabetically.
```sql
SELECT name
FROM people
-- WHERE
ORDER BY name
```

- Get the names of people, sorted by birth date.
```sql
SELECT name
FROM people
-- WHERE
ORDER BY birthdate
```

- Get the birth date and name for every person, in order of when they were born.
```sql
SELECT birthdate, name
FROM people
-- WHERE
ORDER BY birthdate
```

## Sorting single columns (2)
Let's get some more practice with ORDER BY!

- Get the title of films released in 2000 or 2012, in the order they were released.
```sql
SELECT title
FROM films
WHERE (release_year = 2000 or release_year = 2012)
ORDER BY release_year;
```

- Get all details for all films except those released in 2015 and order them by duration.
```sql
SELECT *
FROM films
WHERE release_year <> 2015
ORDER BY duration;
```

- Get the title and gross earnings for movies which begin with the letter 'M' and order the results alphabetically
```sql
SELECT title, gross
FROM films
WHERE title LIKE 'M%'
ORDER BY title;
```

## Sorting single columns (DESC)
To order results in descending order, you can put the keyword DESC after your ORDER BY. For example, to get all the names in the people table, in reverse alphabetical order:



```sql
SELECT name
FROM people
ORDER BY name DESC;
```
Now practice using ORDER BY with DESC to sort single columns in descending order!


- Get the IMDB score and film ID for every film from the reviews table, sorted from highest to lowest score.
```sql
SELECT imdb_score,film_id
FROM reviews
-- WHERE
ORDER BY imdb_score DESC;
```

- Get the title for every film, in reverse order.
```sql
SELECT title
FROM films
-- WHERE
ORDER BY title DESC;
```

- Get the title and duration for every film, in order of longest duration to shortest.
```sql
SELECT title, duration
FROM films
-- WHERE
ORDER BY duration DESC;
```

## Sorting multiple columns
ORDER BY can also be used to sort on multiple columns. It will sort by the first column specified, then sort by the next, then the next, and so on. For example,

```sql
SELECT birthdate, name
FROM people
ORDER BY birthdate, name;
```
sorts on birth dates first (oldest to newest) and then sorts on the names in alphabetical order. **The order of columns is important!**

Try using `ORDER BY` to sort multiple columns! Remember, to specify multiple columns you separate the column names with a comma


- Get the birth date and name of people in the people table, in order of when they were born and alphabetically by name.
```sql
SELECT birthdate, name
FROM people
--WHERE
ORDER BY birthdate, name;
```

- Get the release year, duration, and title of films ordered by their release year and duration.
```sql
SELECT release_year,duration, title
FROM films
--WHERE
ORDER BY release_year, duration;
```

- Get certifications, release years, and titles of films ordered by certification (alphabetically) and release year.
```sql
SELECT certification, release_year, title
FROM films
--WHERE
ORDER BY certification,release_year;
```

- Get the names and birthdates of people ordered by name and birth date.
```sql
SELECT name, birthdate
FROM people
--WHERE
ORDER BY name, birthdate;
```

## GROUP BY
Now you know how to sort results! Often you'll need to aggregate results. For example, you might want to count the number of male and female employees in your company. Here, what you want is to group all the males together and count them, and group all the females together and count them. In SQL, GROUP BY allows you to group a result by one or more columns, like so:



```sql
SELECT sex, count(*)
FROM employees
GROUP BY sex;
```
This might give, for example:



```table
sex	count
male	15
female	19
```
Commonly, GROUP BY is used with aggregate functions like COUNT() or MAX(). Note that GROUP BY always goes after the FROM clause!

## GROUP BY practice
As you've just seen, combining aggregate functions with GROUP BY can yield some powerful results!

A word of warning: SQL will return an error if you try to SELECT a field that is not in your GROUP BY clause without using it to calculate some kind of value about the entire group.

Note that you can combine GROUP BY with ORDER BY to group your results, calculate something about them, and then order your results. For example,

```sql
SELECT sex, count(*)
FROM employees
GROUP BY sex
ORDER BY count DESC;
```
might return something like

```table
sex	count
female	19
male	15
```
because there are more females at our company than males. Note also that ORDER BY always goes after GROUP BY. Let's try some exercises!


- Get the release year and count of films released in each year.
```sql
SELECT release_year, COUNT(*)
FROM films
--WHERE
GROUP BY release_year
-- ORDER BY
```


- Get the release year and average duration of all films, grouped by release year.
```sql
SELECT release_year, AVG(duration)
FROM films
--WHERE
GROUP BY release_year
-- ORDER BY
```

- Get the release year and largest budget for all films, grouped by release year.
```sql
SELECT release_year, MAX(budget)
FROM films
--WHERE
GROUP BY release_year
-- ORDER BY
```

- Get the IMDB score and count of film reviews grouped by IMDB score in the reviews table.
```sql
SELECT imdb_score, COUNT(*)
FROM reviews
--WHERE
GROUP BY imdb_score
-- ORDER BY
```

## GROUP BY practice (2)
Now practice your new skills by combining GROUP BY and ORDER BY with some more aggregate functions!

Make sure to always put the ORDER BY clause at the end of your query. You can't sort values that you haven't calculated yet!



- Get the release year and lowest gross earnings per release year.
```sql
SELECT release_year, MIN(gross)
FROM films
--WHERE
GROUP BY release_year
--ORDER BY
```

- Get the language and total gross amount films in each language made.
```sql
SELECT language, SUM(gross)
FROM films
--WHERE
GROUP BY language
--ORDER BY
```

- Get the country and total budget spent making movies in each country.
```sql
SELECT country, SUM(budget)
FROM films
--WHERE
GROUP BY country
--ORDER BY
```

- Get the release year, country, and highest budget spent making a film for each year, for each country. Sort your results by release year and country.
```sql
SELECT release_year, country, MAX(budget)
FROM films
--WHERE
GROUP BY country, release_year
ORDER BY  release_year, country
```

- Get the country, release year, and lowest amount grossed per release year per country. Order your results by country and release year.
```sql
SELECT release_year, country, MIN(gross)
FROM films
--WHERE
GROUP BY release_year, country
ORDER BY  country, release_year
```

## HAVING a great time
In SQL, aggregate functions can't be used in WHERE clauses. For example, the following query is invalid

```sql
SELECT release_year
FROM films
GROUP BY release_year
WHERE COUNT(title) > 10;
```

This means that if you want to filter based on the result of an aggregate function, you need another way! That's where the HAVING clause comes in. For example,
```sql
SELECT release_year
FROM films
GROUP BY release_year
HAVING COUNT(title) > 10;
```
## All together now
Time to practice using ORDER BY, GROUP BY and HAVING together.

Now you're going to write a query that returns the average budget and average gross earnings for films in each year after 1990, if the average budget is greater than $60 million.

This is going to be a big query, but you can handle it!

- Get the release year, budget and gross earnings for each film in the films table.
```sql
SELECT release_year, budget, gross
FROM films
-- WHERE
-- GROUP BY
-- ORDER BY
-- HAVING
```

-
```sql
SELECT release_year, budget, gross
FROM films
WHERE release_year > 1990
-- GROUP BY
-- ORDER BY
-- HAVING
```

- Remove the budget and gross columns, and group your results by release year.
```sql
SELECT release_year
FROM films
WHERE release_year > 1990
GROUP BY release_year
-- ORDER BY
-- HAVING
```

- Modify your query to include the average budget and average gross earnings for the results you have so far. Alias the average budget as avg_budget; alias the average gross earnings as avg_gross.

```sql
SELECT release_year, AVG(budget) as avg_budget,
AVG(gross) as avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year
-- ORDER BY
-- HAVING
```


-  Modify your query so that only years with an average budget of greater than $60 million are included.
```sql
SELECT 
    release_year,
    AVG(budget) as avg_budget,
    AVG(gross) as avg_gross
FROM
    films
WHERE 
    release_year > 1990
GROUP BY 
    release_year
-- ORDER BY
HAVING AVG(budget) > 60000000
```

- Finally, modify your query to order the results from highest average gross earnings to lowest.
```sql
SELECT 
    release_year,
    AVG(budget) as avg_budget,
    AVG(gross) as avg_gross
FROM
    films
WHERE 
    release_year > 1990
GROUP BY 
    release_year
HAVING AVG(budget) > 60000000
ORDER BY avg_gross DESC;
```


## All together now (2)
Great work! Now try another large query. This time, all in one go!

Remember, if you only want to return a certain number of results, you can use the LIMIT keyword to limit the number of rows returned

- Get the country, average budget, and average gross take of countries that have made more than 10 films. Order the result by country name, and limit the number of results displayed to 5. You should alias the averages as avg_budget and avg_gross respectively.

```sql
-- select country, average budget, average gross
SELECT 
    country, 
    AVG(budget) as avg_budget, 
    AVG(gross) as avg_gross
-- from the films table
FROM 
    films
-- group by country 
GROUP BY
    country
-- where the country has more than 10 titles
HAVING  COUNT(title) > 10
-- order by country
ORDER BY 
    country
-- limit to only show 5 results
LIMIT 5
```



