# SQLBolt
There are queries for section 7 from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_with_outer_joins).

## OUTER JOINs

1. 
Find the list of all buildings that have employees.
```sql
  SELECT DISTINCT building FROM employees
```
2. 
Find the list of all buildings and their capacity.
```sql
  SELECT * FROM buildings
```
3. 
List all buildings and the distinct employee roles in each building (including empty buildings).
```sql
  SELECT DISTINCT building_name, role FROM buildings
    LEFT JOIN employees ON building = building_name
```