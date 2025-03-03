# SQLBolt
There are queries for section 11 from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_with_aggregates_pt_2).

## Queries with aggregates (Pt. 2)

1. 
Find the number of Artists in the studio (without a HAVING clause).
```sql
  SELECT COUNT(name) AS Number FROM employees
    WHERE role = 'Artist'
```
2. 
Find the number of Employees of each role in the studio.
```sql
  SELECT role, COUNT(name) AS Number FROM employees
    GROUP BY role
```
3. 
Find the total number of employee years worked in each building.
```sql
  SELECT SUM(years_employed) AS Total FROM employees
    WHERE role = 'Engineer'
```