# MySQL GROUP BY

In this tutorial we will show how to use `GROUP BY` clause with _aggregate functions_.

Also read [this article](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html) from MySQL.

## Create a dataset

create table

```sql
mysql> create table workers (name varchar(50), category varchar(10), salary float);
```
load dataset
```sql
mysql> load data local infile '/path/workers.txt' into table workers FIELDS TERMINATED BY ',';
```
```txt
John,Python,10500
Peter,Javascript,11200
Mark,Ruby,13000
Anne,PHP,11400
Sammy,Javascript,12800
Alicia,Ruby,17000
Mary,Python,11400
Tina,PHP,9500
Bob,PHP,8000
Kirst,Python,12000
```
## Aggregate functions

* `AVG()`   Return the average value of the argument 
* `COUNT()`   Return a count of the number of rows returned
* `COUNT(DISTINCT)`   Return the count of a number of different values
* `MAX()`   Return the maximum value
* `MIN()`   Return the minimum value
* `SUM()`   Return the sum 

## Syntax
1. Unique value
```sql
select FUNCTION(FIELD) from TABLE;
```
1. List of records
```sql
select [FIELDS], FUNCTION(FIELD) from TABLE group by [FIELD];
```
1. Using `HAVING` (filter the aggregate result)
```sql
select [FIELDS], FUNCTION(FIELD) from TABLE group by [FIELD] having FUNCTION(FIELD) > 10;
```
## Examples

```sql
mysql> select count(salary) from workers;
+---------------+
| count(salary) |
+---------------+
|            10 |
+---------------+
1 row in set (0.01 sec)
```
```sql
mysql> select sum(salary) from workers;
+-------------+
| sum(salary) |
+-------------+
|      116800 |
+-------------+
1 row in set (0.00 sec)
```
```sql
mysql> select avg(salary) from workers;
+-------------+
| avg(salary) |
+-------------+
|       11680 |
+-------------+
1 row in set (0.00 sec)
```
```sql
mysql> select max(salary) from workers;
+-------------+
| max(salary) |
+-------------+
|       17000 |
+-------------+
1 row in set (0.00 sec)
```
```sql
mysql> select min(salary) from workers;
+-------------+
| min(salary) |
+-------------+
|        8000 |
+-------------+
1 row in set (0.00 sec)
```

## Examples with `GROUP BY`

```sql
mysql> select category, sum(salary) from workers group by category;
+------------+-------------+
| category   | sum(salary) |
+------------+-------------+
| Javascript |       24000 |
| PHP        |       28900 |
| Python     |       33900 |
| Ruby       |       30000 |
+------------+-------------+
4 rows in set (0.01 sec)
```
```sql
mysql> select category, avg(salary) from workers group by category;
+------------+-------------------+
| category   | avg(salary)       |
+------------+-------------------+
| Javascript |             12000 |
| PHP        | 9633.333333333334 |
| Python     |             11300 |
| Ruby       |             15000 |
+------------+-------------------+
4 rows in set (0.02 sec)
```
```sql
mysql> select category, count(salary) from workers group by category;
+------------+---------------+
| category   | count(salary) |
+------------+---------------+
| Javascript |             2 |
| PHP        |             3 |
| Python     |             3 |
| Ruby       |             2 |
+------------+---------------+
```

## Examples with `HAVING`

Show the sum of salary of a category if this sum exceeds 30000.
```sql
mysql> select category, sum(salary) from workers group by category having sum(salary) > 30000;
+----------+-------------+
| category | sum(salary) |
+----------+-------------+
| Python   |       33900 |
+----------+-------------+
1 row in set (0.00 sec)
```
Show the sum of salaries where the category has more than two workers.
```sql
mysql> select category, sum(salary) from workers group by category having count(salary) > 2;
+----------+-------------+
| category | sum(salary) |
+----------+-------------+
| PHP      |       28900 |
| Python   |       33900 |
+----------+-------------+
2 rows in set (0.00 sec)
```