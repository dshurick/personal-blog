---
bookShowToc: true
---

# Interview Questions

## SQL

### Resources:

* https://data36.com/sql-interview-questions-tech-screening-data-analysts/

### Question 1

Let’s say you have two SQL tables: `authors` and `books`.

The authors dataset has 1M+ rows; here’s the first six rows:

| author_name | book_name |
|-------------|-----------|
| author_1    | book_1    |
| author_1    | book_2    |
| author_2    | book_3    |
| author_2    | book_4    |
| author_2    | book_5    |
| author_3    | book_6    |
| ...         | ...       |

The books dataset also has 1M+ rows and here’s the first six:

| book_name | sold_copies |
|-----------|------------:|
| book_1    |        1000 |
| book_2    |        1500 |
| book_3    |       34000 |
| book_4    |       29000 |
| book_5    |       40000 |
| book_6    |        4400 |
| ...       | ...         |

Create an SQL query that shows the TOP 3 authors who sold the most books in total!

#### Question 1 Answer

The solution code is:

```sql
SELECT authors.author_name, SUM(books.sold_copies) AS sold_sum
FROM authors
JOIN books
ON books.book_name = authors.book_name
GROUP BY authors.author_name
ORDER BY sold_sum DESC
LIMIT 3;
```

And here is a short explanation:

1. First you have to initiate the JOIN. I joined the two tables by using:

```sql
SELECT *
FROM authors
JOIN books
ON books.book_name = authors.book_name;
```

2. After that, I used a `SUM()` function with a `GROUP BY` clause. This means that in the `SELECT` statement I had to replace the `*` with the `author_name` and `sold_copies` columns. (It’s not mandatory to indicate from which table you are selecting the columns, but it’s worth it. That’s why I used `authors.author_name` and `books.sold_copies`.)

3. Eventually, I `ORDER`ed the results in `DESC`ending order. (Just for my convenience, I also renamed the `sum` column to `sold_sum` using the `AS sold_sum` method in the `SELECT` statement.)

### Question 2

You work for a startup that makes an online presentation software. You have an event log that records every time a user inserted an image into a presentation. (One user can insert multiple images.) The event_log SQL table looks like this:

| user_id | event_date_time |
|---------|----------------:|
| 7494212 |      1535308430 |
| 7494212 |      1535308433 |
| 1475185 |      1535308444 |
| 6946725 |      1535308475 |
| 6946725 |      1535308476 |
| 6946725 |      1535308477 |
| ...     | ...             |

…and it has over one billion rows.

Note: If the `event_date_time` column’s format doesn’t look familiar, google “epoch timestamp”!

Write an SQL query to find out how many users inserted more than 1000 but less than 2000 images in their presentations!

#### Question 2 Answer

The SQL query is:

```sql
SELECT COUNT(*) FROM
  (SELECT user_id, COUNT(event_date_time) AS image_per_user
  FROM event_log
  GROUP BY user_id) AS image_per_user
WHERE image_per_user < 2000 AND image_per_user > 1000;
```

The trick in this task is that you had to use the `COUNT()` function two times: first, you had to count the number of images per user, then the number of users (who fulfill the given condition). The easiest way to do that is to use a subquery.

1. Write the inner query first! Run a simple COUNT() function with a GROUP BY clause on the event_log table.
2. Make sure that you create an alias for the subquery (AS image_per_user). It’s a syntax requirement in SQL.
3. Eventually, in an outer query, apply a WHERE filter and a COUNT() function on the result of the subquery.

### Question 3

You have two SQL tables! The first one is called employees and it contains the employee names, the unique employee ids and the department names of a company. Sample:

| department_name | employee_id |     employee_name |
|-----------------|------------:|------------------:|
| Sales           |         123 |          John Doe |
| Sales           |         211 |        Jane Smith |
| HR              |         556 |         Billy Bob |
| Sales           |         711 |      Robert Hayek |
| Marketing       |         235 |    Edward Jorgson |
| Marketing       |         236 | Christine Packard |
| ...             |         ... |               ... |

The second one is named salaries. It holds the same employee names and the same employee ids – and the salaries for each employee. Sample:

| salary | employee_id |     employee_name |
|-------:|------------:|------------------:|
|    500 |         123 |          John Doe |
|    600 |         211 |        Jane Smith |
|   1000 |         556 |         Billy Bob |
|    400 |         711 |      Robert Hayek |
|   1200 |         235 |    Edward Jorgson |
|    200 |         236 | Christine Packard |
| ...    | ...         | ...               |

The company has 546 employees, so both tables have 546 rows.

Print every department where the average salary per employee is lower than $500!

#### Question 3 Answer

Solution:

```sql
SELECT department_name, AVG(salaries.salary) AS avg_salaries
FROM employees
JOIN salaries
ON employees.employee_id = salaries.employee_id
GROUP BY department_name
HAVING AVG(salaries.salary) < 500;
```

Note: You can solve this task using a subquery, too – but in an interview situation the committee will like the above solution better.

Brief explanation:

1. First JOIN the two tables:

```sql
SELECT *
FROM employees
JOIN salaries
ON employees.employee_id = salaries.employee_id;
```

Watch out! Use the `employee_id` column – not the `employee_name`. (You can always have two John Does at a company, but the employee id is unique!)

2. Then use an `AVG()` function with a `GROUP BY` clause — and replace the `*` with the appropriate columns. (Just like in the first task.)

3. And the last step is to use a `HAVING` clause to filter by the result of the `AVG()` function. (Remember: `WHERE` is not good here because it would be initiated before the `AVG()` function.)
Watch out: in the `HAVING` line, you can’t refer to the alias – you have to use the whole function itself again!
