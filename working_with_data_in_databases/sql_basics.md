# SQL Tutorial from Mode

# BASIC SQL

## SQL SELECT
### Basic syntax: SELECT and FROM
There are two required ingredients in any SQL query: `SELECT` and `FROM`—and they have to be in that order. SELECT indicates which columns you’d like to view, and FROM identifies the table that they live in.

Let’s start by looking at a couple columns from the housing unit table:




### Practice problem:
Write a query to select all of the columns in tutorial.us_housing_units and rename them so that their first letters are capitalized.

```sql
SELECT year AS "Year", 
      month AS "Month",
      month_name AS "Month name",
      south AS "South",
      west AS "West", 
      midwest AS "Midwest",
      northeast AS "Northeast"
  FROM tutorial.us_housing_units
```


## SQL LIMIT



### Why should you limit your results?
Many analysts use limits as a simple way to keep their queries from taking too long to return. The aim of many of your queries will simply be to see what a particular table looks like—you’ll want to scan the first few rows of data to get an idea of which fields you care about and how you want to manipulate them. If you query a very large table (such as one with hundreds of thousands or millions of rows) and don’t use a limit, you could end up waiting a long time for all of your results to be displayed, which doesn’t make sense if you only care about the first few.


### Using the SQL LIMIT command
The limiting functionality is built into Mode to prevent you from accidentally returning millions of rows without meaning to (we’ve all done it). However, if you’re ever using SQL outside of Mode, you can manually add a limit with a SQL command. The following syntax does the same thing as having the box checked with a value of 100:

```sql
SELECT *
FROM tutorial.us_housing_units 
LIMIT 100
```

#### Practice problem
Write a query that uses the LIMIT command to restrict the result set to only 15 rows.

```sql
SELECT *
FROM tutorial.us_housing_units 
LIMIT 15

```

## SQL WHERE

### The SQL WHERE clause
Start by running a `SELECT` statement to re-familiarize yourself with the housing data used in this tutorial. Remember to switch over to Mode and run any of the code you see in the light blue boxes to get a sense of what the output will look like

```sql
SELECT * FROM tutorial.us_housing_units
```
Once you know how to view some data using SELECT and FROM, the next step is filtering the data using the WHERE clause. Here’s what it looks like:

```sql
SELECT *
  FROM tutorial.us_housing_units
 WHERE month = 1
 ```

> Note: the clauses always need to be in this order: SELECT, FROM, WHERE.

## How does WHERE work?
The SQL WHERE clause works in a plain-English way: the above query does the same thing as `SELECT * FROM tutorial.us_housing_units`, except that the results will only include rows where the month column contains the value 1.

In Excel, it’s possible to sort data in such a way that one column can be reordered without reordering any of the other columns—though that could badly scramble your data. When using SQL, entire rows of data are preserved together. If you write a WHERE clause that filters based on values in one column, you’ll limit the results in all columns to rows that satisfy the condition. The idea is that each row is one data point or observation, and all the information contained in that row belongs together.

You can filter your results in a number of ways using comparison and logical operators, which you’ll learn about in the next lesson.



