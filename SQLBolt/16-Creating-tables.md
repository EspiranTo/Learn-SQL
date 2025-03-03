# SQLBolt
There are queries for section 16 from website [SQLBolt](https://sqlbolt.com/lesson/creating_tables).

## Creating tables

1. 
Create a new table named Database with the following columns:
– **Name** A string (text) describing the name of the database
– **Version** A number (floating point) of the latest version of this database
– **Download_count** An integer count of the number of times this database was downloaded

This table has no constraints.
```sql
  CREATE TABLE Database (
    Name TEXT,
    Version FLOAT,
    Download_count INTEGER
);
```