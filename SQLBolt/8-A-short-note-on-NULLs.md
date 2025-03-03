# SQLBolt
There are queries for section 8 from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_with_nulls).

## A short note on NULLs

1. 
Find the name and role of all employees who have not been assigned to a building.
```sql
  SELECT name, role FROM employees
    WHERE building IS NULL
```
2. 
Find the names of the buildings that hold no employees.
```sql
  SELECT DISTINCT building_name FROM buildings
    LEFT JOIN employees ON building = building_name
    WHERE name IS NULL
```