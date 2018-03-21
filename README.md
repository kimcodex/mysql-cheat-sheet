# MySQL Quick Reference
#### Commands:

|  Action |  Statement |
| ------------ | ------------ |
|  List of all DB: | `SHOW DATABASES;`  |
|  Create DB: | `CREATE DATABASE database;`  |
|  Use a DB: |  `USE database;` |
|  List all tables in DB: |  `SHOW database;` |
|  Show the structure of a table: | `DESCRIBE table; SHOW COLUMNS FROM table;`|
|  Delete DB: |  `DROP DATABASE databasename;` |
----
### Modify
| Action  |Statement   |Example   |
| ------------ | ------------ | ------------ |
| Create table  | `CREATE TABLE table (`<br>&nbsp;&nbsp;&nbsp;`column1 type [[NOT] NULL] `<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;` [AUTO_INCREMENT],`<br> &nbsp;&nbsp;&nbsp;`column2 type [[NOT] NULL]`<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`  [AUTO_INCREMENT],`<br>&nbsp;&nbsp;&nbsp;`...`<br>&nbsp;&nbsp;&nbsp;`PRIMARY KEY (column(s))    );` | `CREATE TABLE Students (`<br>&nbsp;&nbsp;&nbsp;`lastname varchar(30) NOT NULL, `<br> &nbsp;&nbsp;&nbsp;`firstname varchar(30) NOT NULL,`<br> &nbsp;&nbsp;&nbsp;`  studentid int NOT NULL,`<br>&nbsp;&nbsp;&nbsp;`PRIMARY KEY (studentid)    );`  |
| Insert Data  |`INSERT INTO table VALUES`<br>&nbsp;&nbsp;&nbsp;` (list of values);`<br>`INSERT INTO table SET`<br>&nbsp;&nbsp;&nbsp;`column1=value1,`<br>&nbsp;&nbsp;&nbsp;`column2=value2,`<br>&nbsp;&nbsp;&nbsp;`..`<br>&nbsp;&nbsp;&nbsp;`columnk=valuek,`<br>`INSERT INTO table`<br>`(column1,column2,...)`<br>&nbsp;&nbsp;&nbsp;`VALUES (value1,value2...);`   |  `INSERT INTO Students VALUES`<br>&nbsp;&nbsp;&nbsp;` ('Smith','John',123);`<br>`INSERT INTO Students SET`<br>&nbsp;&nbsp;&nbsp;`firstname='John',`<br>&nbsp;&nbsp;&nbsp;`lastname='Smith',`<br>&nbsp;&nbsp;&nbsp;`studentid=123,`<br>`INSERT INTO Students`<br>`(studentid,firstname,lastname)`<br>&nbsp;&nbsp;&nbsp;`VALUES (123,'John','Smith');`  |
|  Insert/Select |`INSERT INTO table`<br>`(column1,column2,...)`<br>&nbsp;&nbsp;&nbsp;`SELECT statement;`<br>&nbsp;&nbsp;&nbsp; |`INSERT INTO Students`<br>`(studentid,firstname,lastname)`<br>&nbsp;&nbsp;&nbsp;`SELECT studentid, firstname, lastname`<br>&nbsp;&nbsp;&nbsp;` FROM OtherStudentTable`<br>&nbsp;&nbsp;&nbsp;`WHERE LastName like '%son';`|
|  Delete Data |   `DELETE FROM table`<br>&nbsp;&nbsp;&nbsp;`[WHERE condition(s)];`<br><br>`(Omit WHERE to delete all data)`  |  `DELETE FROM Students `<br>&nbsp;&nbsp;&nbsp;`WHERE lastname='Smith';`<br>`DELETE FROM Students `<br>&nbsp;&nbsp;&nbsp;`WHERE lastname like '%Smith%';`<br>&nbsp;&nbsp;&nbsp;`AND firstname='John';`<br>`DELETE FROM Students;`  |
|Updating Data   |  `UPDATE table SET`<br>&nbsp;&nbsp;&nbsp;`column1=value1,`<br>&nbsp;&nbsp;&nbsp;`column2=value2,`<br>&nbsp;&nbsp;&nbsp;`...`<br>&nbsp;&nbsp;&nbsp;`columnk=valuek,`<br>&nbsp;&nbsp;&nbsp;` [WHERE condition(s)];` |  `UPDATE Students SET`<br>&nbsp;&nbsp;&nbsp;`lastname='Jones'WHERE,`<br>&nbsp;&nbsp;&nbsp;`studentid=124,`<br>`UPDATE Students SET`<br>&nbsp;&nbsp;&nbsp;`lastname='Jones' major='Theatre'`<br>&nbsp;&nbsp;&nbsp;`WHERE studentid=124 OR`<br>&nbsp;&nbsp;&nbsp;`(major='Art' AND firstname='Pete');`  |
| Insert column  | `ALTER TABLE table ADD `<br>&nbsp;&nbsp;&nbsp;`COLUMN column  type options;`|  `ALTER TABLE Students ADD COLUMN `<br>&nbsp;&nbsp;&nbsp;`hometown varchar(20);`|
|  Delete column |  `ALTER TABLE table DROP COLUMN column;` |`ALTER TABLE Students DROP COLUMN Dorm;`   |
|  Delete table (Careful!) |`DROP TABLE [IF EXISTS] table;`   |  `DROP TABLE Animals;` |
----
### SELECT query
| Action  |Statement   | Example   |
| ------------ | ------------ | ------------ |
| All columns  | `SELECT * FROM table;`  | `SELECT * FROM Students;`  |
| Some columns   |  `SELECT column1,column2,... FROM table;` | `SELECT LastName, FirstName FROM Students;`  |
|  Some rows/columns | `SELECT column1,column2,...`<br>&nbsp;&nbsp;&nbsp;`FROM table [WHERE condition(s)];`  | `SELECT LastName,FirstName`<br>&nbsp;&nbsp;&nbsp;`FROM Students WHERE StudentID LIKE '%123%';`  |
|  No Repeats | `SELECT [DISTINCT] column(s) FROM table;` | `SELECT DISTINCT LastName FROM Students;`  |
|  Ordering |  `	SELECT column1,column2,...`<br>&nbsp;&nbsp;&nbsp;` FROM table [ORDER BY column(s [DESC]];` | `SELECT LastName,FirstName`<br>&nbsp;&nbsp;&nbsp;`FROM Students`<br>&nbsp;&nbsp;&nbsp;`ORDER BY LastName, FirstName DESC;` |
| Column Aliases  |`SELECT column1 [AS alias1],`<br>&nbsp;&nbsp;&nbsp;`column2 [AS alias2], ...`<br>&nbsp;&nbsp;&nbsp;`FROM table1;`   |`SELECT LastName,FirstName AS First`<br>&nbsp;&nbsp;&nbsp;`FROM Students;` |
| Grouping  | `SELECT column1,column2,...`<br>&nbsp;&nbsp;&nbsp;`FROM table [GROUP BY column(s)];`  | `SELECT LastName,COUNT(*)` <br>&nbsp;&nbsp;&nbsp; ` FROM StudentsGROUP BY LastName;`|
| Group Filtering  |`SELECT column1,column2,...`<br>&nbsp;&nbsp;&nbsp;`FROM table`<br>&nbsp;&nbsp;&nbsp;`[GROUP BY column(s)]`<br>&nbsp;&nbsp;&nbsp;`[HAVING condition(s)];`   | `SELECT LastName,COUNT(*)`<br>&nbsp;&nbsp;&nbsp;`FROM Students`<br>&nbsp;&nbsp;&nbsp;`GROUP BY LastName`<br>&nbsp;&nbsp;&nbsp;`HAVING LastName like '%son';`   |
|  Joins |  `SELECT column1,column2,...`<br>&nbsp;&nbsp;&nbsp;`FROM table1,table2,...`<br>&nbsp;&nbsp;&nbsp;`[WHERE condition(s)];` |  `SELECT LastName,Points`<br>&nbsp;&nbsp;&nbsp;`FROM Students,Assignments `<br>&nbsp;&nbsp;&nbsp;`WHERE AssignmentID=12 AND`<br>`Students.StudentID=Assignments.StudentID;` |
|  Table Aliases | `SELECT column1,column2,...`<br>&nbsp;&nbsp;&nbsp;`FROM table1 [alias1], table2 [alias2],...`<br>&nbsp;&nbsp;&nbsp;`[WHERE condition(s)];`  |`SELECT LastName,Points,`<br>&nbsp;&nbsp;&nbsp;`FROM Students S, Assignments A`<br>&nbsp;&nbsp;&nbsp;`WHERE S.StudentID=A.StudentID AND A.AssignmentID=12;`    |
|  Everything |`SELECT [DISTINCT] column1 [AS alias1], column2 [AS alias2], ...`<br>&nbsp;&nbsp;&nbsp;`FROM table1 [alias1], table2 [alias2],...`<br>&nbsp;&nbsp;&nbsp;`[WHERE condition(s)] [GROUP BY column(s)]`<br>&nbsp;&nbsp;&nbsp;`[HAVING condition(s)] [ORDER BY column(s) [DESC]];`   | `SELECT Points, Count(*) AS Cnt`<br>&nbsp;&nbsp;&nbsp;`FROM Students S, Assignments A`<br>&nbsp;&nbsp;&nbsp;`WHERE S.StudentsID=A.StudentID`<br>&nbsp;&nbsp;&nbsp;`AND  A.AssignmentID=12`<br>&nbsp;&nbsp;&nbsp;` GROUP BY Points`<br>&nbsp;&nbsp;&nbsp;`HAVING Points > 10 ORDER BY Cnt DESC;`  |

