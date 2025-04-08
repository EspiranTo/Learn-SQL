There are queries for database Dormitory.

### Easy Questions
1. Which dormitories are in the database?
```sql
  SELECT name FROM dormitories
```
2. What is the capacity of room 101?
```sql
  SELECT capacity FROM rooms
    WHERE number = 101
```
3. How many students live in each dormitory?
```sql
  SELECT name, COUNT(student_id) AS student_count FROM dormitories
    JOIN rooms ON dormitories.dormitory_id = rooms.dormitory_id
    JOIN accommodation ON rooms.number = accommodation.room_number
    GROUP BY dormitories.dormitory_id, dormitories.name
```
4. Which students pay the accommodation fee?
```sql
  SELECT full_name FROM students
    JOIN payments ON students.student_id = payments.student_id
    WHERE status = 'paid'
```
5. Which employees work at the Vlkova dormitory?
```sql
  SELECT full_name FROM staff
    JOIN dormitories ON staff.dormitory_id = dormitories.dormitory_id
    WHERE name = 'Vlkova'
```
### Harder Questions
6. Which students live in the men's rooms on the first floor?
```sql
  SELECT full_name FROM students
    JOIN accommodation ON students.student_id = accommodation.student_id
    JOIN rooms ON accommodation.room_number = rooms.number
    WHERE type = 'men' AND floor = 1
```
7. Which students have paid for housing after January 1, 2025?
```sql
  SELECT full_name FROM students
    JOIN payments ON students.student_id = payments.student_id
    WHERE payment_date > '2024-04-03'
```
8. What is the total amount paid by all students for accommodation in the Vlkova dormitory?
```sql
  SELECT SUM(amount) AS total_payment FROM payments
    JOIN accommodation ON payments.student_id = accommodation.student_id
    JOIN rooms ON accommodation.room_number = rooms.number
    JOIN dormitories ON rooms.dormitory_id = dormitories.dormitory_id
    WHERE name = 'Vlkova'
```
9. Which rooms have free spaces (when the number of students in a room is less than its capacity)?
```sql
  SELECT number, capacity - COUNT(student_id) AS free_spaces FROM rooms
    JOIN accommodation ON rooms.number = accommodation.room_number
    GROUP BY number, capacity
    HAVING (capacity - COUNT(student_id)) > 0
```
10. Which employee holds the position of Cleaner in the dormitory with the largest capacity?
```sql
  SELECT full_name FROM staff
    JOIN dormitories ON staff.dormitory_id = dormitories.dormitory_id
    WHERE capacity = (SELECT MAX(capacity) FROM dormitories)
      AND position = 'Cleaner'
```