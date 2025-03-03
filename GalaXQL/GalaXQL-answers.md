# GalaXQL
There are queries for tasks from website [GalaXQL](https://solhsa.com/g3/).

## Sections:
1. [SELECT](#select)
2. [SELECT FROM](#select-from)
3. [SELECT FROM, WHERE, ORDER BY DESC](#select-from-where-order-by-desc)
4. [MAX, MIN, COUNT, AVG, SUM, NULL](#max-min-count-avg-sum-null)
5. [INSERT INTO VALUES](#insert-into-values)
6. [INSERT INTO SELECT](#insert-into-select)
7. [Transactions, DELETE FROM WHERE](#transactions-delete-from-where)
8. [UPDATE SET WHERE](#update-set-where)
9. [SELECT FROM table1, table2, DISTINCT](#select-from-table1-table2-distinct)
10. [SELECT FROM (SELECT FROM)](#select-from-select-from)
11. [SELECT FROM JOIN](#select-from-join)
12. [CREATE VIEW, DROP VIEW](#create-view-drop-view)
13. [CREATE TABLE, DROP TABLE](#create-table-drop-table)
14. [Constraints](#constraints)
15. [ALTER TABLE](#alter-table)
16. [SELECT, GROUP BY, HAVING](#select-group-by-having)
17. [UNION, UNION ALL, INTERSECT, EXCEPT](#union-union-all-intersect-except)
18. [Triggers](#triggers)
19. [Indexes](#indexes)

## SELECT
Use SQL to calculate the number of seconds in one day (where day is 24 hours, hour is 60 minutes and a minute is 60 seconds).
```sql
  SELECT 24*60*60
```
## SELECT FROM
Get x, y and z information from all the rows from the table 'stars'.
```sql
  SELECT x, y, z FROM stars
```
## SELECT FROM, WHERE, ORDER BY DESC
Make a query which returns starid, x, y and z for all stars where x is greater than zero and starid is less than one hundred. Sort the results by the y-coordinate so that the smallest values come first.
```sql
  SELECT starid, x, y, z FROM stars
    WHERE x > 0 AND starid < 100
    ORDER BY y ASC
```
## MAX, MIN, COUNT, AVG, SUM, NULL
Build a query where you calculate the sum of all y values divided by all x values.
```sql
  SELECT SUM(y/x) FROM stars
```
## INSERT INTO VALUES
Hilight five stars which have star id between 5000 and 15000, and have class 7.
```sql
  DELETE FROM hilight;
  SELECT * FROM stars
    WHERE starid BETWEEN 5000 AND 15000 AND class = 7;

  INSERT INTO hilight VALUES (5007), (5048), (5050), (5068), (5075);
```
## INSERT INTO SELECT
Hilight all the stars with starid between 10000 and 11000. (I know, this is not too difficult, but it looks neat).
```sql
  INSERT INTO hilight SELECT starid FROM stars
	  WHERE starid BETWEEN 10000 AND 11000;
```
## Transactions, DELETE FROM WHERE
Kill off all stars with starid lower than 10000. Do this inside a transaction, so that when I run the ROLLBACK command, we're back with the original galaxy.
```sql
  BEGIN;
  
  DELETE FROM stars WHERE starid < 10000
```
## UPDATE SET WHERE
Starting from the normal galaxy, update it so that you swap the x and z coordinates for stars which have star id between 10000 and 15000.
```sql
  BEGIN;

  UPDATE stars
  SET x = z,
      z = x
  WHERE starid BETWEEN 10000 AND 15000
```
## SELECT FROM table1, table2, DISTINCT
Hilight all stars with starid of at least 20000, which have planets with moons that have an orbit distance of at least 3000.
```sql
  BEGIN;

  INSERT INTO hilight
  SELECT DISTINCT stars.starid FROM stars, planets, moons
    WHERE stars.starid > 20000
      AND stars.starid = planets.starid
      AND planets.planetid = moons.planetid
      AND moons.orbitdistance > 3000
```
## SELECT FROM (SELECT FROM)
Hilight the star (or stars) which has the planet with the highest orbit distance in the galaxy.
```sql
  BEGIN;

  INSERT INTO hilight 
  SELECT stars.starid FROM stars, planets, 
    ( SELECT MAX(orbitdistance) AS max FROM planets ) 
      WHERE planets.orbitdistance = max AND planets.starid = stars.starid;
```
## SELECT FROM JOIN
Generate a list of stars with star ids between 500 and 600 (but not including 500 and 600) with columns "starname", "startemp", "planetname", and "planettemp". The list should have all stars, with the unknown data filled out with NULL. These values are, as usual, fictional. Calculate the temperature for a star with ((class+7)*intensity)*1000000, and a planet's temperature is calculated from the star's temperature minus 50 times orbit distance.
```sql
  SELECT stars.name AS starname,
    (stars.class + 7) * stars.intensity * 1000000 AS startemp, 
    planets.name AS planetname, 
    ((stars.class + 7) * stars.intensity * 1000000) - (50 * planets.orbitDistance) AS planettemp
    FROM stars
    LEFT OUTER JOIN planets ON planets.starId = stars.starId
      WHERE stars.starId > 500 AND stars.starId < 600
```
## CREATE VIEW, DROP VIEW
Create a VIEW called "numbers" with the columns "three", "intensity" and "x", where "x" and "intensity" come from the stars table, "three" contains the number 3 on all rows. For additional fun, sort the whole thing by "x" - although I won't care.
```sql
  CREATE VIEW numbers AS
    SELECT 3 AS three, intensity, x FROM stars
    ORDER BY x DESC
```
## CREATE TABLE, DROP TABLE
Create a table named 'colors' with the columns 'color' and 'description'. Color is integer, description is text. Populate the table with color values from -3 to 10; each star class has its own color; fill the description with something.
```sql
  CREATE TABLE colors (color INTEGER, description TEXT);
  INSERT INTO colors
  VALUES (-3, 'Red'),
	       (-2, 'Pink'),
         (-1, 'Orange'),
         (0, 'Yellow'),
         (1, 'Purple'),
         (2, 'Brown'),
         (3, 'Black'),
         (4, 'Gray'),
         (5, 'White'),
         (6, 'Green'),
         (7, 'Blue'),
         (8, 'Cyan'),
         (9, 'Magenta'),
         (10, 'Violet');
```
## Constraints
Create a table called "quotes" with two columns: "id", which is primary key, and takes integers, and "quote" which contains non-null text strings, such as quote of the day (http://www.qotd.org/). Fill in a couple of rows so that I have something to query for.
```sql
  CREATE TABLE quotes (id INTEGER PRIMARY KEY, quote TEXT NOT NULL);
  INSERT INTO quotes
  VALUES (1, 'Cosmonautics has a limitless future, and its prospects are as limitless as the universe itself!'),
         (2, 'The cosmos is like the kindest and most intelligent animal. Not a single atom of the universe can escape the sensations of higher intelligent life.');
```
## ALTER TABLE
First, create and populate a table using this command. Rename the table to 'my_table', and add a column called 'moredata'. Add one whole new row and change the 'moredata' value of at least one existing row.
```sql
  CREATE TABLE alter_test (id INTEGER PRIMARY KEY, data TEXT NOT NULL);
  INSERT INTO alter_test (data) VALUES ('Foo'), ('Bar'), ('Baz');

  ALTER TABLE alter_test RENAME TO my_table;
  ALTER TABLE my_table ADD COLUMN moredata TEXT;

  UPDATE my_table SET moredata = 'New Data'
    WHERE id BETWEEN 1 AND 3;
```
## SELECT, GROUP BY, HAVING
Hilight the star with the most orbitals (combined planets and moons). If multiple stars have the highest number of orbitals, highlight the one with the lowest star id.
```sql
  CREATE TABLE v_orbital (starid INTEGER, orbitals INTEGER);
  INSERT INTO v_orbital SELECT stars.starid, COUNT(planets.planetid) + COUNT(moons.planetid)
    AS orbitals FROM stars
  LEFT OUTER JOIN planets ON stars.starid = planets.starid
  LEFT OUTER JOIN moons ON planets.planetid = moons.planetid
  GROUP BY stars.starid;

  INSERT INTO hilight SELECT starid FROM v_orbital
  WHERE orbitals = ( SELECT MAX(orbitals) FROM v_orbital );

  DROP TABLE IF EXIST v_orbital;
```
## UNION, UNION ALL, INTERSECT, EXCEPT
Build a query which returns starids from planets.
The starids should be selected so that for each starid (x) in the list:
- there should exist a planet with a starid that's three times x
but
- there should not exist a planet with starid two times x.
Only use starids from the planets table.
```sql
  SELECT starid FROM planets
  INTERSECT
  SELECT 3 * starid FROM planets
  EXCEPT
  SELECT 2 * starid FROM planets
```
## Triggers
Create a trigger which, when a new star is created, clears the hilight table and inserts the new star id to the hilight table.
```sql
  CREATE TRIGGER after_insert_star
  AFTER INSERT ON stars
  FOR EACH ROW
  BEGIN
    DELETE FROM hilight;
    INSERT INTO hilight (starid) VALUES (NEW.starid);
  END
```
## Indexes
Use ALTER TABLE to rename the 'gateway' table to 'gateways'.
```sql
  ALTER TABLE gateway RENAME TO gateways
```