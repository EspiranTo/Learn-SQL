# Database "Dormitory"
This is the code to create a database and tables in it, as well as fill these tables with dates.

Creating database.
```sql
DROP DATABASE IF EXISTS Dormitory;
CREATE DATABASE Dormitory;
```

Creating table "dormitories".
```sql
DROP TABLE IF EXISTS dormitories;
CREATE TABLE dormitories (
    dormitory_id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    address VARCHAR(100) NOT NULL,
    psc INT NOT NULL,
    capacity INT NOT NULL
);
```

Filling the table "dormitories" with data.
```sql
INSERT INTO dormitories(dormitory_id, name, address, psc, capacity)
	   VALUES (1, 'Vlkova', 'Vlkova 810/43, Praha 3 - Zizkov', 13000, 50),
			  (2, 'Tesla', 'Ve Smeckach 603/13, Praha 1 - Nove Mesto', 11000, 98),
			  (3, 'Dejvicka', 'Zikova 538/19, Praha 6 - Dejvice', 16000, 132),
			  (4, 'Hvezda', 'Zvonickova 1927/7, Praha 6 - Liboc', 16200, 120),
		      (5, 'Orlik', 'Jindrisska 907/10, Praha 1 - Nove Mesto', 11000, 85),
			  (6, 'Sazava', 'Jizni Mesto, Blazimska 1781/4, Praha 4', 14900, 150),
			  (7, 'Volha', 'K Verneraku 950, Praha 4 - Chodov', 14800, 200),
			  (8, 'Strahov', 'Vanickova 315/7, Praha 6 - Strahov', 16900, 450),
			  (9, 'Sinkule', 'Zikova 702/13, Praha 6 - Dejvice', 16000, 75),
			  (10, 'Kolej 17. listopadu', 'Petrzilkova 2583/1, Praha 13 - Stodulky', 15500, 110);
```

Creating table "rooms".
```sql
DROP TABLE IF EXISTS rooms;
CREATE TABLE rooms (
    room_id INT PRIMARY KEY,
    dormitory_id INT NOT NULL,
    number INT UNIQUE NOT NULL,
    floor INT NOT NULL,
    capacity INT NOT NULL,
    type VARCHAR(10) NOT NULL,
    CONSTRAINT CK_room_type CHECK (type IN ('men', 'women')),
    CONSTRAINT FK_rooms_dormitories FOREIGN KEY (dormitory_id) REFERENCES dormitories(dormitory_id) ON DELETE CASCADE
);
```

Filling the table "rooms" with data.
```sql
INSERT INTO rooms (room_id, dormitory_id, number, floor, capacity, type)
	   VALUES (1, 1, 101, 1, 2, 'men'),
			  (2, 1, 102, 1, 3, 'women'),
			  (3, 1, 201, 2, 2, 'men'),
			  (4, 1, 202, 2, 4, 'women'),
			  (5, 1, 301, 3, 3, 'men'),
			  (6, 1, 302, 3, 2, 'women'),
			  (7, 2, 103, 1, 2, 'men'),
			  (8, 2, 104, 1, 3, 'women'),
			  (9, 2, 203, 2, 2, 'men'),
			  (10, 2, 204, 2, 4, 'women'),
			  (11, 2, 303, 3, 3, 'men'),
			  (12, 2, 304, 3, 2, 'women'),
			  (13, 3, 105, 1, 2, 'men'),
			  (14, 3, 106, 1, 3, 'women'),
			  (15, 3, 205, 2, 2, 'men'),
			  (16, 3, 206, 2, 4, 'women'),
			  (17, 3, 305, 3, 3, 'men'),
			  (18, 3, 306, 3, 2, 'women'),
			  (19, 4, 107, 1, 2, 'men'),
			  (20, 4, 108, 1, 3, 'women'),
			  (21, 4, 207, 2, 2, 'men'),
			  (22, 4, 208, 2, 4, 'women'),
			  (23, 4, 307, 3, 3, 'men'),
			  (24, 4, 308, 3, 2, 'women'),
			  (25, 5, 109, 1, 2, 'men'),
			  (26, 5, 110, 1, 3, 'women'),
			  (27, 5, 209, 2, 2, 'men'),
			  (28, 5, 210, 2, 4, 'women'),
			  (29, 5, 309, 3, 3, 'men'),
			  (30, 5, 310, 3, 2, 'women'),
			  (31, 6, 111, 1, 2, 'men'),
			  (32, 6, 112, 1, 3, 'women'),
			  (33, 6, 211, 2, 2, 'men'),
			  (34, 6, 212, 2, 4, 'women'),
			  (35, 6, 311, 3, 3, 'men'),
			  (36, 6, 312, 3, 2, 'women'),
			  (37, 7, 113, 1, 2, 'men'),
			  (38, 7, 114, 1, 3, 'women'),
			  (39, 7, 213, 2, 2, 'men'),
			  (40, 7, 214, 2, 4, 'women'),
			  (41, 7, 313, 3, 3, 'men'),
			  (42, 7, 314, 3, 2, 'women'),
			  (43, 8, 115, 1, 2, 'men'),
			  (44, 8, 116, 1, 3, 'women'),
			  (45, 8, 215, 2, 2, 'men'),
			  (46, 8, 216, 2, 4, 'women'),
			  (47, 8, 315, 3, 3, 'men'),
			  (48, 8, 316, 3, 2, 'women'),
			  (49, 9, 117, 1, 2, 'men'),
			  (50, 9, 118, 1, 3, 'women'),
			  (51, 9, 217, 2, 2, 'men'),
			  (52, 9, 218, 2, 4, 'women'),
			  (53, 9, 317, 3, 3, 'men'),
			  (54, 9, 318, 3, 2, 'women'),
			  (55, 10, 119, 1, 2, 'men'),
			  (56, 10, 120, 1, 3, 'women'),
			  (57, 10, 219, 2, 2, 'men'),
			  (58, 10, 220, 2, 4, 'women'),
			  (59, 10, 319, 3, 3, 'men'),
			  (60, 10, 320, 3, 2, 'women');
```

Creating table "students".
```sql
DROP TABLE IF EXISTS students;
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    full_name VARCHAR(50) NOT NULL,
    gender VARCHAR(10) NOT NULL,
    date_of_birth DATE NOT NULL,
	phone VARCHAR(50) NOT NULL,
	email VARCHAR(50) NOT NULL,
	university_group VARCHAR(50) NOT NULL,
	faculty VARCHAR(50) NOT NULL,
	CONSTRAINT CK_student_gender CHECK (gender IN ('male', 'female')),
);
```

Filling the table "students" with data.
```sql
INSERT INTO students (student_id, full_name, gender, date_of_birth, phone, email, university_group, faculty)
       VALUES (1, 'Alex Johnson', 'male', '2002-04-15', '+12345678901', 'alex.johnson@email.com', 'CS101', 'Computer Science'),
              (2, 'Michael Smith', 'male', '2001-07-22', '+12345678902', 'michael.smith@email.com', 'CS102', 'Computer Science'),
              (3, 'John Doe', 'male', '2000-12-05', '+12345678903', 'john.doe@email.com', 'EE101', 'Electrical Engineering'),
              (4, 'David Brown', 'male', '2003-03-18', '+12345678904', 'david.brown@email.com', 'EE102', 'Electrical Engineering'),
              (5, 'James Wilson', 'male', '2002-06-29', '+12345678905', 'james.wilson@email.com', 'ME101', 'Mechanical Engineering'),
              (6, 'Robert Moore', 'male', '2001-11-14', '+12345678906', 'robert.moore@email.com', 'ME102', 'Mechanical Engineering'),
              (7, 'William Taylor', 'male', '2003-02-07', '+12345678907', 'william.taylor@email.com', 'Math101', 'Mathematics'),
              (8, 'Christopher Anderson', 'male', '2002-08-23', '+12345678908', 'christopher.anderson@email.com', 'Math102', 'Mathematics'),
              (9, 'Daniel Thomas', 'male', '2001-05-30', '+12345678909', 'daniel.thomas@email.com', 'Bio101', 'Biology'),
              (10, 'Matthew Martinez', 'male', '2000-09-12', '+12345678910', 'matthew.martinez@email.com', 'Bio102', 'Biology'),
              (11, 'Joshua White', 'male', '2003-07-15', '+12345678911', 'joshua.white@email.com', 'Physics101', 'Physics'),
              (12, 'Andrew Harris', 'male', '2002-10-28', '+12345678912', 'andrew.harris@email.com', 'Physics102', 'Physics'),
              (13, 'Joseph Clark', 'male', '2001-03-03', '+12345678913', 'joseph.clark@email.com', 'Chemistry101', 'Chemistry'),
              (14, 'Ryan Lewis', 'male', '2000-06-18', '+12345678914', 'ryan.lewis@email.com', 'Chemistry102', 'Chemistry'),
              (15, 'Brandon Walker', 'male', '2003-09-25', '+12345678915', 'brandon.walker@email.com', 'Architecture101', 'Architecture'),
              (16, 'Kevin Hall', 'male', '2002-12-09', '+12345678916', 'kevin.hall@email.com', 'Architecture102', 'Architecture'),
              (17, 'Jacob Allen', 'male', '2001-04-22', '+12345678917', 'jacob.allen@email.com', 'Law101', 'Law'),
              (18, 'Ethan Young', 'male', '2000-08-17', '+12345678918', 'ethan.young@email.com', 'Law102', 'Law'),
              (19, 'Nicholas King', 'male', '2003-01-05', '+12345678919', 'nicholas.king@email.com', 'Medical101', 'Medicine'),
              (20, 'Tyler Wright', 'male', '2002-05-20', '+12345678920', 'tyler.wright@email.com', 'Medical102', 'Medicine'),
              (21, 'Zachary Lopez', 'male', '2001-07-03', '+12345678921', 'zachary.lopez@email.com', 'Law103', 'Law'),
              (22, 'Jonathan Scott', 'male', '2000-10-11', '+12345678922', 'jonathan.scott@email.com', 'Law104', 'Law'),
              (23, 'Samuel Green', 'male', '2003-03-14', '+12345678923', 'samuel.green@email.com', 'Medical103', 'Medicine'),
              (24, 'Benjamin Adams', 'male', '2002-09-06', '+12345678924', 'benjamin.adams@email.com', 'Medical104', 'Medicine'),
              (25, 'Patrick Nelson', 'male', '2001-11-29', '+12345678925', 'patrick.nelson@email.com', 'Medical105', 'Medicine'),
              (26, 'Emily Brown', 'female', '2002-01-10', '+12345678926', 'emily.brown@email.com', 'Bio103', 'Biology'),
              (27, 'Sarah Miller', 'female', '2001-04-18', '+12345678927', 'sarah.miller@email.com', 'Bio104', 'Biology'),
              (28, 'Jessica Wilson', 'female', '2000-07-25', '+12345678928', 'jessica.wilson@email.com', 'CS103', 'Computer Science'),
              (29, 'Ashley Davis', 'female', '2003-03-29', '+12345678929', 'ashley.davis@email.com', 'CS104', 'Computer Science'),
              (30, 'Amanda Garcia', 'female', '2002-06-10', '+12345678930', 'amanda.garcia@email.com', 'EE103', 'Electrical Engineering'),
              (31, 'Samantha Rodriguez', 'female', '2001-09-12', '+12345678931', 'samantha.rodriguez@email.com', 'EE104', 'Electrical Engineering'),
              (32, 'Megan Martinez', 'female', '2000-11-15', '+12345678932', 'megan.martinez@email.com', 'ME103', 'Mechanical Engineering'),
              (33, 'Hannah Taylor', 'female', '2003-02-22', '+12345678933', 'hannah.taylor@email.com', 'ME104', 'Mechanical Engineering'),
              (34, 'Lauren Thomas', 'female', '2002-05-07', '+12345678934', 'lauren.thomas@email.com', 'Math103', 'Mathematics'),
              (35, 'Rachel Hernandez', 'female', '2001-08-30', '+12345678935', 'rachel.hernandez@email.com', 'Math104', 'Mathematics'),
              (36, 'Brittany Moore', 'female', '2000-12-01', '+12345678936', 'brittany.moore@email.com', 'Physics103', 'Physics'),
              (37, 'Olivia White', 'female', '2003-06-05', '+12345678937', 'olivia.white@email.com', 'Physics104', 'Physics'),
              (38, 'Natalie Allen', 'female', '2002-10-14', '+12345678938', 'natalie.allen@email.com', 'Chemistry103', 'Chemistry'),
              (39, 'Victoria King', 'female', '2001-01-09', '+12345678939', 'victoria.king@email.com', 'Chemistry104', 'Chemistry'),
              (40, 'Kayla Scott', 'female', '2000-04-27', '+12345678940', 'kayla.scott@email.com', 'Architecture103', 'Architecture'),
              (41, 'Alyssa Green', 'female', '2003-09-08', '+12345678941', 'alyssa.green@email.com', 'Architecture104', 'Architecture'),
              (42, 'Taylor Nelson', 'female', '2002-07-11', '+12345678942', 'taylor.nelson@email.com', 'Law104', 'Law'),
              (43, 'Jasmine Baker', 'female', '2001-03-22', '+12345678943', 'jasmine.baker@email.com', 'Law105', 'Law'),
              (44, 'Morgan Hall', 'female', '2000-06-15', '+12345678944', 'morgan.hall@email.com', 'Medical106', 'Medicine'),
              (45, 'Brooke Adams', 'female', '2003-08-17', '+12345678945', 'brooke.adams@email.com', 'Medical107', 'Medicine'),
              (46, 'Stephanie Wright', 'female', '2002-09-21', '+12345678946', 'stephanie.wright@email.com', 'Bio105', 'Biology'),
              (47, 'Haley Lopez', 'female', '2001-10-30', '+12345678947', 'haley.lopez@email.com', 'CS105', 'Computer Science'),
              (48, 'Vanessa Rivera', 'female', '2000-12-05', '+12345678948', 'vanessa.rivera@email.com', 'CS106', 'Computer Science'),
              (49, 'Savannah Perez', 'female', '2003-05-29', '+12345678949', 'savannah.perez@email.com', 'EE105', 'Electrical Engineering'),
              (50, 'Madison Carter', 'female', '2002-11-02', '+12345678950', 'madison.carter@email.com', 'EE106', 'Electrical Engineering');
```

Creating table "accommodation".
```sql
DROP TABLE IF EXISTS accommodation;
CREATE TABLE accommodation (
    accommodation_id INT PRIMARY KEY,
    student_id INT NOT NULL,
    room_number INT NOT NULL,
    check_in_date DATE NOT NULL,
    check_out_date DATE,
    CONSTRAINT FK_accommodation_student FOREIGN KEY (student_id) REFERENCES students(student_id) ON DELETE CASCADE,
    CONSTRAINT FK_accommodation_room FOREIGN KEY (room_number) REFERENCES rooms(number) ON DELETE CASCADE
);
```

Filling the table "accommodation" with data.
```sql
INSERT INTO accommodation (accommodation_id, student_id, room_number, check_in_date, check_out_date)
       VALUES (1, 1, 101, '2024-09-01', NULL),
              (2, 2, 103, '2023-09-10', '2025-06-30'),
              (3, 3, 105, '2022-08-25', NULL),
              (4, 4, 107, '2024-09-01', NULL),
              (5, 5, 109, '2023-09-05', NULL),
              (6, 6, 111, '2022-08-15', '2024-05-15'),
              (7, 7, 113, '2024-09-01', NULL),
              (8, 8, 115, '2023-09-08', NULL),
              (9, 9, 117, '2022-08-20', NULL),
              (10, 10, 119, '2021-09-01', '2024-06-01'),
              (11, 11, 201, '2024-09-05', NULL),
              (12, 12, 203, '2023-09-12', NULL),
              (13, 13, 205, '2022-08-22', '2024-07-10'),
              (14, 14, 207, '2021-09-10', NULL),
              (15, 15, 209, '2024-09-07', NULL),
              (16, 16, 211, '2023-09-15', '2024-05-30'),
              (17, 17, 213, '2022-08-30', NULL),
              (18, 18, 215, '2021-09-12', '2024-06-15'),
              (19, 19, 217, '2024-09-09', NULL),
              (20, 20, 219, '2023-09-18', '2024-07-01'),
              (21, 21, 301, '2022-08-28', '2024-06-20'),
              (22, 22, 303, '2021-09-15', NULL),
              (23, 23, 305, '2024-09-11', NULL),
              (24, 24, 307, '2023-09-20', '2024-05-20'),
              (25, 25, 309, '2022-08-31', '2024-06-10'),
              (26, 26, 102, '2024-09-02', NULL),
              (27, 27, 104, '2023-09-11', '2024-06-30'),
              (28, 28, 106, '2022-08-27', '2024-05-25'),
              (29, 29, 108, '2024-09-03', NULL),
              (30, 30, 110, '2023-09-06', NULL),
              (31, 31, 112, '2022-08-19', NULL),
              (32, 32, 114, '2021-09-03', '2024-07-05'),
              (33, 33, 116, '2024-09-04', NULL),
              (34, 34, 118, '2023-09-09', NULL),
              (35, 35, 120, '2022-08-21', NULL),
              (36, 36, 202, '2021-09-07', '2024-06-05'),
              (37, 37, 204, '2024-09-06', NULL),
              (38, 38, 206, '2023-09-14', NULL),
              (39, 39, 208, '2022-08-24', NULL),
              (40, 40, 210, '2021-09-11', '2024-05-15'),
              (41, 41, 212, '2024-09-08', NULL),
              (42, 42, 214, '2023-09-16', NULL),
              (43, 43, 216, '2022-08-29', NULL),
              (44, 44, 218, '2021-09-13', NULL),
              (45, 45, 220, '2024-09-10', NULL),
              (46, 46, 302, '2023-09-19', '2024-07-12'),
              (47, 47, 304, '2022-08-26', NULL),
              (48, 48, 306, '2021-09-16', NULL),
              (49, 49, 308, '2024-09-12', NULL),
              (50, 50, 310, '2023-09-21', '2024-06-25');
```

Creating table "payments".
```sql
DROP TABLE IF EXISTS payments;
CREATE TABLE payments (
    payment_id INT PRIMARY KEY,
    student_id INT NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    payment_date DATE NOT NULL,
    payment_method VARCHAR(10) NOT NULL,
    status VARCHAR(10) NOT NULL,
	CONSTRAINT CK_payment_payment_method CHECK (payment_method IN ('card', 'cash')),
	CONSTRAINT CK_payment_status CHECK (status IN ('paid', 'expired')),
	CONSTRAINT FK_payments_students FOREIGN KEY (student_id) REFERENCES students(student_id) ON DELETE CASCADE
);
```

Filling the table "payments" with data.
```sql
INSERT INTO payments (payment_id, student_id, amount, payment_date, payment_method, status)
       VALUES (1, 1, 1500.00, '2024-01-10', 'card', 'paid'),
              (2, 2, 1200.50, '2024-02-12', 'cash', 'paid'),
              (3, 3, 1350.75, '2024-03-05', 'card', 'paid'),
              (4, 4, 1400.00, '2024-03-10', 'cash', 'paid'),
              (5, 5, 1250.25, '2024-04-15', 'card', 'paid'),
              (6, 6, 1100.00, '2024-05-20', 'cash', 'paid'),
              (7, 7, 1450.50, '2024-06-01', 'card', 'paid'),
              (8, 8, 1550.00, '2024-06-15', 'cash', 'paid'),
              (9, 9, 1300.80, '2024-07-03', 'card', 'paid'),
              (10, 10, 1200.00, '2024-08-08', 'cash', 'paid'),
              (11, 11, 1400.50, '2024-09-12', 'card', 'paid'),
              (12, 12, 1250.75, '2024-10-04', 'cash', 'paid'),
              (13, 13, 1450.00, '2024-11-16', 'card', 'paid'),
              (14, 14, 1500.00, '2024-12-05', 'cash', 'paid'),
              (15, 15, 1325.50, '2024-01-28', 'card', 'paid'),
              (16, 16, 1380.00, '2024-02-18', 'cash', 'paid'),
              (17, 17, 1455.75, '2024-03-09', 'card', 'paid'),
              (18, 18, 1200.00, '2024-03-30', 'cash', 'paid'),
              (19, 19, 1330.25, '2024-04-25', 'card', 'paid'),
              (20, 20, 1265.50, '2024-05-18', 'cash', 'paid'),
              (21, 21, 1350.00, '2024-06-06', 'card', 'paid'),
              (22, 22, 1400.00, '2024-07-14', 'cash', 'paid'),
              (23, 23, 1200.00, '2024-08-20', 'card', 'paid'),
              (24, 24, 1305.50, '2024-09-28', 'cash', 'paid'),
              (25, 25, 1250.00, '2024-10-22', 'card', 'paid'),
              (26, 26, 1450.50, '2024-11-07', 'cash', 'paid'),
              (27, 27, 1375.00, '2024-12-01', 'card', 'paid'),
              (28, 28, 1300.00, '2024-01-20', 'cash', 'paid'),
              (29, 29, 1400.00, '2024-02-25', 'card', 'paid'),
              (30, 30, 1225.50, '2024-03-14', 'cash', 'paid'),
              (31, 31, 1500.00, '2024-04-01', 'card', 'paid'),
              (32, 32, 1350.25, '2024-05-10', 'cash', 'paid'),
              (33, 33, 1250.00, '2024-06-23', 'card', 'paid'),
              (34, 34, 1325.75, '2024-07-05', 'cash', 'paid'),
              (35, 35, 1400.00, '2024-08-15', 'card', 'paid'),
              (36, 36, 1300.25, '2024-09-02', 'cash', 'paid'),
              (37, 37, 1450.50, '2024-09-18', 'card', 'paid'),
              (38, 38, 1200.00, '2024-10-30', 'cash', 'paid'),
              (39, 39, 1305.00, '2024-11-12', 'card', 'paid'),
              (40, 40, 1250.00, '2024-12-02', 'cash', 'paid'),
              (41, 41, 1325.50, '2024-01-10', 'card', 'paid'),
              (42, 42, 1400.00, '2024-02-14', 'cash', 'paid'),
              (43, 43, 1500.00, '2024-03-08', 'card', 'paid'),
              (44, 44, 1300.50, '2024-04-13', 'cash', 'paid'),
              (45, 45, 1200.00, '2024-05-22', 'card', 'paid'),
              (46, 46, 1350.00, '2024-06-11', 'cash', 'paid'),
              (47, 47, 1450.50, '2024-07-01', 'card', 'paid'),
              (48, 48, 1200.00, '2024-08-09', 'cash', 'paid'),
              (49, 49, 1300.25, '2024-09-21', 'card', 'paid'),
              (50, 50, 1400.00, '2024-10-25', 'cash', 'paid');
```

Creating table "staff".
```sql
DROP TABLE IF EXISTS staff;
CREATE TABLE staff (
    staff_id INT PRIMARY KEY,
    full_name VARCHAR(50) NOT NULL,
    position VARCHAR(50) NOT NULL,
    phone VARCHAR(50) NOT NULL,
    dormitory_id INT NOT NULL,
    gender VARCHAR(10) NOT NULL,
    CONSTRAINT FK_staff_dormitory FOREIGN KEY (dormitory_id) REFERENCES dormitories(dormitory_id) ON DELETE CASCADE
);
```

Filling the table "staff" with data.
```sql
INSERT INTO staff (staff_id, full_name, position, phone, dormitory_id, gender)
       VALUES (1, 'Ivan Ivanov', 'Director', '+79001234567', 1, 'male'),
              (2, 'Maria Petrova', 'Cleaner', '+79002345678', 1, 'female'),
              (3, 'Alexey Smirnov', 'Cleaner', '+79003456789', 1, 'male'),
              (4, 'Natalia Kuznetsova', 'Security Guard', '+79004567890', 1, 'female'),
              (5, 'Maxim Lebedev', 'Repairman', '+79005678901', 1, 'male'),
              (6, 'Olga Grigorieva', 'Cook', '+79006789012', 1, 'female'),
              (7, 'Dmitry Solovyev', 'Cook', '+79007890123', 1, 'male'),
              (8, 'Alina Petrova', 'Director', '+79002345679', 2, 'female'),
              (9, 'Svetlana Chernova', 'Cleaner', '+79003456790', 2, 'female'),
              (10, 'Sergey Grigoriev', 'Cleaner', '+79004567891', 2, 'male'),
              (11, 'Andrey Ivanov', 'Security Guard', '+79005678902', 2, 'male'),
              (12, 'Vladimir Shevchenko', 'Repairman', '+79006789013', 2, 'male'),
              (13, 'Valentina Zaitseva', 'Cook', '+79007890124', 2, 'female'),
              (14, 'Kirill Nikolaev', 'Cook', '+79008901234', 2, 'male'),
              (15, 'Irina Alexeeva', 'Director', '+79000123456', 3, 'female'),
              (16, 'Tatiana Bykova', 'Cleaner', '+79001234567', 3, 'female'),
              (17, 'Vladimir Zakharov', 'Cleaner', '+79002345678', 3, 'male'),
              (18, 'Sergey Petrov', 'Security Guard', '+79003456789', 3, 'male'),
              (19, 'Evgeny Vasiliev', 'Repairman', '+79004567890', 3, 'male'),
              (20, 'Ekaterina Karpova', 'Cook', '+79005668901', 3, 'female'),
              (21, 'Dmitry Kozlov', 'Cook', '+79006789012', 3, 'male'),
              (22, 'Viktor Mikhailov', 'Director', '+79007890123', 4, 'male'),
              (23, 'Ekaterina Kozlova', 'Cleaner', '+79008901234', 4, 'female'),
              (24, 'Alexander Timofeev', 'Cleaner', '+79009012345', 4, 'male'),
              (25, 'Artem Chernov', 'Security Guard', '+79000123456', 4, 'male'),
              (26, 'Denis Fedorov', 'Repairman', '+79001234567', 4, 'male'),
              (27, 'Olga Shcherbakova', 'Cook', '+79002345678', 4, 'female'),
              (28, 'Vladislav Rudenko', 'Cook', '+79003456789', 4, 'male'),
              (29, 'Galina Dmitrieva', 'Director', '+79004567890', 5, 'female'),
              (30, 'Natalia Savelieva', 'Cleaner', '+79005678901', 5, 'female'),
              (31, 'Alexey Gerasimov', 'Cleaner', '+79006789012', 5, 'male'),
              (32, 'Pavel Kalinin', 'Security Guard', '+79007890123', 5, 'male'),
              (33, 'Igor Rebrov', 'Repairman', '+79008901234', 5, 'male'),
              (34, 'Irina Goryacheva', 'Cook', '+79009012345', 5, 'female'),
              (35, 'Darina Kirillova', 'Cook', '+79000123456', 5, 'female'),
              (36, 'Oleg Ponomarev', 'Director', '+79002345679', 6, 'male'),
              (37, 'Valentina Antonova', 'Cleaner', '+79003456790', 6, 'female'),
              (38, 'Victor Popov', 'Cleaner', '+79004567891', 6, 'male'),
              (39, 'Boris Kovalenko', 'Security Guard', '+79005678902', 6, 'male'),
              (40, 'Vladimir Frolov', 'Repairman', '+79006789013', 6, 'male'),
              (41, 'Yulia Ilina', 'Cook', '+79007890124', 6, 'female'),
              (42, 'Petr Morozov', 'Cook', '+79008901234', 6, 'male'),
              (43, 'Anastasia Orlova', 'Director', '+79000123456', 7, 'female'),
              (44, 'Elena Vasilieva', 'Cleaner', '+79001234567', 7, 'female'),
              (45, 'Kirill Semenov', 'Cleaner', '+79002345678', 7, 'male'),
              (46, 'Oleg Pavlov', 'Security Guard', '+79003456789', 7, 'male'),
              (47, 'Alexey Komarov', 'Repairman', '+79004567890', 7, 'male'),
              (48, 'Liliya Vykhodtseva', 'Cook', '+79005678901', 7, 'female'),
              (49, 'Semyon Volkov', 'Cook', '+79006789012', 7, 'male'),
              (50, 'Dmitry Alexandrov', 'Director', '+79007890123', 8, 'male'),
              (51, 'Marina Ivanova', 'Cleaner', '+79008901234', 8, 'female'),
              (52, 'Denis Filippov', 'Cleaner', '+79009012345', 8, 'male'),
              (53, 'Viktor Antonov', 'Security Guard', '+79000123456', 8, 'male'),
              (54, 'Evgeny Petrov', 'Repairman', '+79001234567', 8, 'male'),
              (55, 'Nina Matveeva', 'Cook', '+79002345678', 8, 'female'),
              (56, 'Andrey Lysenko', 'Cook', '+79003456789', 8, 'male'),
              (57, 'Sergey Markov', 'Director', '+79004567890', 9, 'male'),
              (58, 'Elena Belova', 'Cleaner', '+79005678901', 9, 'female'),
              (59, 'Antonina Smirnova', 'Cleaner', '+79006789012', 9, 'female'),
              (60, 'Igor Tarasov', 'Security Guard', '+79007890123', 9, 'male'),
              (61, 'Dmitry Kolesnikov', 'Repairman', '+79008901234', 9, 'male'),
              (62, 'Olga Akimova', 'Cook', '+79009012345', 9, 'female'),
              (63, 'Artem Borodin', 'Cook', '+79000123456', 9, 'male'),
              (64, 'Yulia Lobanova', 'Director', '+79002345679', 10, 'female'),
              (65, 'Oksana Baranova', 'Cleaner', '+79003456790', 10, 'female'),
              (66, 'Vitaly Baranov', 'Cleaner', '+79004567891', 10, 'male'),
              (67, 'Nikita Klimov', 'Security Guard', '+79005678902', 10, 'male'),
              (68, 'Boris Ryabov', 'Repairman', '+79006789013', 10, 'male'),
              (69, 'Svetlana Egorova', 'Cook', '+79007890124', 10, 'female'),
              (70, 'Sergey Makarov', 'Cook', '+79008901234', 10, 'male');
```