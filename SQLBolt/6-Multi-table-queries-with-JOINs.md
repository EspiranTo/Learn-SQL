# SQLBolt
There are queries for section 6 from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_with_joins).

## Multi-table queries with JOINs

1. 
Find the domestic and international sales for each movie.
```sql
  SELECT title, domestic_sales, international_sales FROM movies
    INNER JOIN boxoffice ON movie_id = id
```
2. 
Show the sales numbers for each movie that did better internationally rather than domestically.
```sql
  SELECT title, domestic_sales, international_sales FROM movies
    INNER JOIN boxoffice ON movie_id = id
    WHERE international_sales > domestic_sales
```
3. 
List all the movies by their ratings in descending order.
```sql
  SELECT title FROM movies
    INNER JOIN boxoffice ON movie_id = id
    ORDER BY rating DESC
```