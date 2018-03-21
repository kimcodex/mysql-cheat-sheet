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


### Data Types
| Data type  |Syntax   | Example  |Comments   |
| ------------ | ------------ | ------------ | ------------ |
|   |  `BIT[(length)]` | `BIT`  |  A bit-value type. *length* indicates the number of bits per value, from 1 to 64. The default is 1 if M is omitted. |
|   |  `TINYINT[(length)] [UNSIGNED] [ZEROFILL]` |   | A very small integer. The signed range is -128 to 127. The unsigned range is 0 to 255.  |
|   |  `SMALLINT[(length)] [UNSIGNED] [ZEROFILL]` |   |  A small integer. The signed range is -32768 to 32767. The unsigned range is 0 to 65535. |
|   | `MEDIUMINT[(length)] [UNSIGNED] [ZEROFILL]`  |   | A medium-sized integer. The signed range is -8388608 to 8388607. The unsigned range is 0 to 16777215.  |
|   |  `INT[(length)] [UNSIGNED] [ZEROFILL]` | `INT(5)`   | A normal-size integer. The signed range is -2147483648 to 2147483647. The unsigned range is 0 to 4294967295.  |
|   | `INTEGER[(length)] [UNSIGNED] [ZEROFILL]`  |   | This type is a synonym for INT.  |
|   |  `BIGINT[(length)] [UNSIGNED] [ZEROFILL]` |   | A large integer. The signed range is -9223372036854775808 to 9223372036854775807. The unsigned range is 0 to 18446744073709551615.  |
|   | `REAL[(length,decimals)] [UNSIGNED] [ZEROFILL]`  |   |   |
| Double-precision floating-point  |  `DOUBLE[(length,decimals)] [UNSIGNED] [ZEROFILL]` |   |  Permissible values are -1.7976931348623157E+308 to -2.2250738585072014E-308, 0, and 2.2250738585072014E-308 to 1.7976931348623157E+308.  |
|  Floating-point (real) numbers |  `FLOAT[(length,decimals)] [UNSIGNED] [ZEROFILL]` |   | Permissible values are -3.402823466E+38 to -1.175494351E-38, 0, and 1.175494351E-38 to 3.402823466E+38.  |
|   | `DECIMAL[(len[,D])] [UNSIGNED] [ZEROFILL]`  |   | A packed “exact” fixed-point number. *len* is the total number of digits (the precision) and *D* is the number of digits after the decimal point (the scale). The decimal point and (for negative numbers) the - sign are not counted in len. If *D* is 0, values have no decimal point or fractional part. The maximum number of digits (*len*) for DECIMAL is 65. The maximum number of supported decimals (*D*) is 30. If *D* is omitted, the default is 0. If *len* is omitted, the default is 10.  |
|   |  `NUMERIC[(length[,decimals])] [UNSIGNED] [ZEROFILL]` |   |   |
|date| `DATE`  |   |  The supported range is '1000-01-01' to '9999-12-31'. MySQL displays DATE values in 'YYYY-MM-DD' format, but permits assignment of values to DATE columns using either strings or numbers. |
|  time |  `TIME` |   | The range is '-838:59:59.000000' to '838:59:59.000000'. MySQL displays TIME values in 'HH:MM:SS[.fraction]' format, but permits assignment of values to TIME columns using either strings or numbers.  |
|  date and time | `TIMESTAMP`  |   | The range is '1970-01-01 00:00:01.000000' UTC to '2038-01-19 03:14:07.999999' UTC. TIMESTAMP values are stored as the number of seconds since the epoch ('1970-01-01 00:00:00' UTC). A TIMESTAMP cannot represent the value '1970-01-01 00:00:00' because that is equivalent to 0 seconds from the epoch and the value 0 is reserved for representing '0000-00-00 00:00:00', the “zero” TIMESTAMP value.  |
|  date and time | `DATETIME`  |   |  The supported range is '1000-01-01 00:00:00.000000' to '9999-12-31 23:59:59.999999'. MySQL displays DATETIME values in 'YYYY-MM-DD HH:MM:SS[.fraction]' format, but permits assignment of values to DATETIME columns using either strings or numbers. |
| year  | `YEAR(4)` |   | A year in four-digit format. MySQL displays YEAR values in YYYY format, but permits assignment of values to YEAR columns using either strings or numbers. Values display as 1901 to 2155, and 0000.  |
| Fixed-length strings  |`CHAR[(length)] `<br>&nbsp;&nbsp;&nbsp;`[BINARY] [CHARACTER SET charset_name]`<br>&nbsp;&nbsp;&nbsp;` [COLLATE collation_name]`   |   |  The range of *length* is 0 to 255. If *length* is omitted, the length is 1.  |
| variable-length string  | `VARCHAR(length) `<br>&nbsp;&nbsp;&nbsp;`[BINARY] [CHARACTER SET charset_name]`<br>&nbsp;&nbsp;&nbsp;` [COLLATE collation_name]`  |   |  The range of M is 0 to 65,535. |
|   | `BINARY[(length)]`  |   | The BINARY type is similar to the CHAR type, but stores binary byte strings rather than nonbinary character strings. An optional length *length* represents the column length in bytes. If omitted, *length* defaults to 1.  |
|   |  `VARBINARY(length)` |   |  The VARBINARY type is similar to the VARCHAR type, but stores binary byte strings rather than nonbinary character strings. *length* represents the maximum column length in bytes. |
|   | `TINYBLOB`  |   | A BLOB column with a maximum length of 255 (28 − 1) bytes. Each TINYBLOB value is stored using a 1-byte length prefix that indicates the number of bytes in the value.  |
|  Binary Large Object  | `BLOB`  |   |A BLOB column with a maximum length of 65,535 (216 − 1) bytes. Each BLOB value is stored using a 2-byte length prefix that indicates the number of bytes in the value.   |
| Binary Large Object  |  `MEDIUMBLOB` |   |  A BLOB column with a maximum length of 16,777,215 (224 − 1) bytes. |
|  Binary Large Object |  `LONGBLOB` |   |  A BLOB column with a maximum length of 4,294,967,295 or 4GB (232 − 1) bytes.  |
|   | `TINYTEXT [BINARY]` <br>&nbsp;&nbsp;&nbsp;`[CHARACTER SET charset_name]`<br>&nbsp;&nbsp;&nbsp;` [COLLATE collation_name]`  |   | A TEXT column with a maximum length of 255 (28 − 1) characters.  |
|   |`TEXT [BINARY]`<br>&nbsp;&nbsp;&nbsp;` [CHARACTER SET charset_name]`<br>&nbsp;&nbsp;&nbsp;`[COLLATE collation_name]`  |   | A TEXT column with a maximum length of 65,535 (216 − 1) characters.  |
|   | `MEDIUMTEXT [BINARY] [CHARACTER SET charset_name] [COLLATE collation_name]`  |   |  A TEXT column with a maximum length of 16,777,215 (224 − 1) characters.  |
|   |  `LONGTEXT [BINARY]`<br>&nbsp;&nbsp;&nbsp;` [CHARACTER SET charset_name]`<br>&nbsp;&nbsp;&nbsp;` [COLLATE collation_name]` |   |  TEXT column with a maximum length of 4,294,967,295 or 4GB (232 − 1) characters.  |
|   | `ENUM(value1,value2,value3,...) `<br>&nbsp;&nbsp;&nbsp;`[CHARACTER SET charset_name]`<br>&nbsp;&nbsp;&nbsp;` [COLLATE collation_name]`  |   | An enumeration. A string object that can have only one value, chosen from the list of values 'value1', 'value2', ..., NULL or the special '' error value. ENUM values are represented internally as integers. An ENUM column can have a maximum of 65,535 distinct elements  |
|   |  `SET(value1,value2,value3,...) `<br>&nbsp;&nbsp;&nbsp;`[CHARACTER SET charset_name]`<br>&nbsp;&nbsp;&nbsp;` [COLLATE collation_name]`| | ASDF|

`SERIAL` is an alias for `BIGINT UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE`.


**Notes: []  means 'optional'


