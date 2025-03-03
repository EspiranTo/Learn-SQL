# SQLBolt
There are queries for section 12 from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_order_of_execution).

## Order of execution of a Query

1. 
Find the number of movies each director has directed.
```sql
  SELECT director, COUNT(title) AS Number FROM movies
    GROUP BY director
```
2. 
Find the total domestic and international sales that can be attributed to each director.
```sql
  SELECT director, SUM(domestic_sales + international_sales) AS Total FROM movies
    INNER JOIN boxoffice ON movie_id = id
    GROUP BY director
```