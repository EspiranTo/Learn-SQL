# SQLBolt
There are queries for section 10 from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_with_aggregates).

## Queries with aggregates (Pt. 1)

1. 
Find the longest time that an employee has been at the studio.
```sql
  SELECT MAX(years_employed) AS Longest FROM employees
```
2. 
For each role, find the average number of years employed by employees in that role.
```sql
  SELECT role, AVG(years_employed) AS Average FROM employees
    GROUP BY role
```
3. 
Find the total number of employee years worked in each building.
```sql
  SELECT building, SUM(years_employed) AS Total FROM employees
    GROUP BY building
```