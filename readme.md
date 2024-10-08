# MySQL cheatsheet

I have even uploaded the .sql file which you can download and directly run them in the sql prompt.

### General Commands

To run sql files

```sql
source <filename>.sql;
```

## Data Types

### Integer Types

- `INT`: Stores standard integers, commonly used for medium-range numbers. Size: 4 bytes.
- `TINYINT`: Stores very small integer values, typically used for boolean-like flags (0 or 1) or small numeric ranges. Size: 1 byte.
- `SMALLINT`: Used for storing small integer values. Suitable for smaller ranges of numbers that don't require a full `INT`. Size: 2 bytes.
- `MEDIUMINT`: A medium-sized integer type, used for ranges larger than `SMALLINT` but smaller than `INT`. Size: 3 bytes.
- `BIGINT`: Stores very large integer values, suitable for numbers larger than what `INT` can handle. Size: 8 bytes.

### Floating-Point Types

- `FLOAT(M,D)`: Stores floating-point numbers with precision. `M` is the total number of digits, and `D` is the number of decimal places. Typically used for non-critical, approximate numeric values.
- `DOUBLE(M,D)`: Similar to `FLOAT`, but with double the precision, used for more accurate floating-point numbers.

### Exact Numeric Types

- `DECIMAL(M,D)`: Stores exact numeric values with fixed precision and scale. `M` is the total number of digits, and `D` is the number of decimal places. Commonly used for financial calculations where precision is crucial.

### Boolean Type

- `BOOLEAN`: Represents a true/false value. Typically stored as `TINYINT(1)` where `1` means true and `0` means false.

### Binary Data Types

- `BINARY(M)`: Stores fixed-length binary data. `M` specifies the number of bytes. Used for fixed-size binary data like UUIDs.
- `VARBINARY(M)`: Stores variable-length binary data up to `M` bytes. Suitable for binary files, encrypted data, etc.

### JSON Type

- `JSON`: Stores JSON (JavaScript Object Notation) data, allowing you to store and query structured data directly within the database. Suitable for flexible, schema-less data.

### Spatial Data Types

- `GEOMETRY`: Represents a point, line, or polygon in a spatial system. Used for geographical and spatial data.
- `POINT`: Represents a single location in a spatial coordinate system, like a latitude and longitude pair.

### UUID (Universally Unique Identifier)

- `UUID`: A 128-bit value used to uniquely identify information across systems. Useful for generating unique keys in distributed systems.

### ENUM Type

- `ENUM('value1', 'value2', ...)`: A string object that can have one of several predefined values. Useful for representing a limited set of choices like status fields or categories.

### Set Type

- `SET('value1', 'value2', ...)`: Similar to `ENUM`, but allows storing multiple values from the predefined list. Useful for multiple-choice fields.

### Date and Time Types

- `DATE`: Stores date values in the format `YYYY-MM-DD`. Suitable for representing dates without time components.
- `DATETIME`: Stores both date and time values in the format `YYYY-MM-DD HH:MM:SS`. Useful for timestamps or events that require both date and time.
- `TIME`: Stores time values in the format `HH:MM:SS`. Ideal for representing durations or time of day without a date.
- `TIMESTAMP`: Similar to `DATETIME`, but includes automatic updating on record changes. Used for tracking when a record was created or last modified.
- `YEAR`: Stores a year value in 2 or 4 digits (e.g., `98` or `1998`). Useful for storing birth years, project start years, etc.

### String Types

- `CHAR(M)`: A fixed-length character string where `M` specifies the number of characters. Suitable for storing data with a predictable and consistent length, such as state codes or country abbreviations.
- `VARCHAR(M)`: A variable-length string where `M` defines the maximum length. Used for text fields where the length of the data varies, such as names or email addresses.
- `BLOB` or `TEXT`: `BLOB` (Binary Large Object) stores large binary data such as images or files. `TEXT` stores large amounts of textual data, suitable for long descriptions or articles.

## Comments

```sql
/* Multi
line
comment */
```

```sql
# Single Line Comment
```

```sql
-- Single Line Comment
```

## Data Definition Language (DDL)

#### Create Database

```sql
create database cheatsheet;
```

#### Use Database

```sql
use cheatsheet;
```

#### Show Databases

```sql
show databases;
```

#### Create Table

```sql
create table employee
(
    employee_id int primary key,              -- Setting primary key(1st method)
    first_name varchar(50),
    last_name varchar(50),
    dept_number int,
    age int,
    salary real
);

create table department
(
    dept_number int,
    dept_name varchar(50),
    dept_location varchar(50),
    emp_id int,
    primary key(dept_number)                -- Setting primary key(2nd method)
);
```

#### Show Tables

```sql
show tables;
```

#### Describe Table

```sql
describe employee;
desc employee;
show columns in employee;
```

#### Rename Table

```sql
rename table employee to employee_table;
alter table employee_table rename to employee;
```

#### Renaming Column

```sql
alter table employee change column employee_id emp_id int;
```

#### Add Constraint to Column

```sql
alter table employee change column first_name first_name varchar(50) not null;
```

#### Add Column

```sql
alter table employee add column salary real;
```

#### Drop Column

```sql
alter table employee drop column salary;
```

#### Modify the Datatype of column

```sql
alter table employee modify column salary int;
```

#### Truncate Table

```sql
truncate employee;
```

#### Drop Table

```sql
drop table department;
```

#### Drop Database

```sql
drop database cheatsheet;
```

## Data Manipulation Language (DML)

#### Insertion (Complete)

```sql
insert into employee (employee_id, first_name, last_name, dept_number, age, salary) values (1, "Anurag", "Peddi", 1, 20, 93425.63);

insert into employee values (2, "Anuhya", "Peddi", 2, 20, 83425.63);
```

#### Insertion (Partial)

```sql
insert into employee (employee_id, first_name) values (3, "Vageesh");
```

#### Updating all rows

```sql
update employee set salary = 1.1 * salary;
```

#### Updating a specified row

```sql
update employee set salary = 1.2 * salary where employee_id = 1;
```

#### Delete a specified row

```sql
delete from employee where employee_id = 2;
```

#### Delete all rows

```sql
delete from employee;
```

#### Enabling foreign key checks

```sql
set foreign_key_checks = 1;
```

#### Disabling foreign key checks

```sql
set foreign_key_checks = 0;
```

## Data Query Language (DQL)

#### Display Table

```sql
select * from employee;
```

#### Select only specified columns

```sql
select employee_id, first_name from employee;
```

#### Select only few rows

```sql
select employee_id, first_name from employee where age > 25;
```

### Where Clause

#### Greater than(>)

```sql
select * from employee where salary > 3100;
```

#### Greater than equal to(>=)

```sql
select * from employee where salary >= 3100;
```

#### Less than(<)

```sql
select * from employee where salary < 4500;
```

#### Less than equal to(<=)

```sql
select * from employee where salary <= 4350;
```

#### Range

```sql
select * from employee where salary > 3000 and salary < 4000;
```

#### BETWEEN and AND

```sql
select * from employee where salary between 3000 and 4000;
```

### OR

```sql
select * from employee where salary = 3000 or salary = 4000;
```

#### Null

```sql
select * from employee where salary is NULL;
```

#### Not null

```sql
select * from employee where salary is NOT NULL;
```

### ORDER BY Clause

```sql
select * from employee ORDER BY salary DESC;
```

#### Like Operator

```sql
select * from employee where name like '%Jo%';          -- Similar to *Jo* in regrex
```

```sql
select * from employee where name like 'Jo_';           -- Similar to Jo. in regrex
```

## Views

#### Create a view

```sql
create view personal_info as select first_name, last_name, age from employees;
```

#### Displaying view

```sql
select * from personal_info;
```

#### Updating in view

```sql
update personal_info set salary = 1.1 * salary;
```

#### Deleting record from view

```sql
delete from personal_info where age < 40;
```

#### Droping a view

```sql
drop view personal_info;
```

## Joins

#### Inner join

```sql
select e.fname, p.pname from employees as e inner join project as p on e.eid = p.eid;

-- or

select e.fname, p.pname from employees as e join project as p on e.eid = p.eid;
```

#### Full outer join

```sql
select e.fname, p.pname from employees as e left outer join project as p on e.eid = p.eid
union
select e.fname, p.pname from employees as e right outer join project as p on e.eid = p.eid;
```

#### Left outer join

```sql
select e.fname, p.pname from employees as e left outer join project as p on e.eid = p.eid;
```

#### Right outer join

```sql
select e.fname, p.pname from employees as e right outer join project as p on e.eid = p.eid;
```

#### Left outer join - inner join

```sql
select e.fname, p.pname from employees as e left outer join project as p on e.eid = p.eid where p.pname is null;
```

#### Right outer join - inner join

```sql
select e.fname, p.pname from employees as e right outer join project as p on e.eid = p.eid where e.fname is null;
```

## Aggregation

#### Sum function

```sql
select sum(population) from city group by population;
```

#### Average function

```sql
select avg(population) from city group by population;
```

#### Count function

```sql
select district, count(district) from city group by district;
```

#### Maximum function

```sql
select max(population) from city group by population;
```

#### Minimum function

```sql
select min(population) from city group by population;
```

#### Standard deviation function

```sql
select stddev(population) from city group by population;
```

#### Group concat function

```sql
select group_concat(population) from city group by population;
```

> Only COUNT function considers NULL values

## Procedure

#### Creating procedure

```sql
create procedure display_dbs()
show databases;
```

#### Calling procedure

```sql
call display_dbs();
```

#### Drop procedure

```sql
drop procedure display_dbs;
```

## Transaction

#### Begin transaction

```sql
start transaction;
```

#### Create savepoint

```sql
savepoint sv_pt;
```

```sql
delete from city;       -- changing data in table
```

#### Rollback

```sql
rollback to sv_pt;
```

#### Releasing savepoint

```sql
release savepoint sv_pt;
```

#### Commiting changes

```sql
commit;
```

## Constraints

#### Not Null

```sql
alter table Employee
change
    Age
    Age int NOT NULL;
```

#### Unique

```sql
alter table Employee
add constraint u_q unique(ID);
```

```sql
alter table Employee -- drop the constraint
drop constraint u_q;
```

#### Primary Key

```sql
alter table Employee
add constraint p_k primary key(ID);
```

```sql
alter table Employee -- drop the constraint
drop constraint p_k;
```

#### Check

```sql
alter table Employee
add constraint Age check (age>=30);
```

```sql
alter table Employee -- drop the constraint
drop check Age;
```

#### Default

```sql
alter table Employee
alter Age set default 10;
```

```sql
alter table Employee -- drop the constraint
alter Age drop default;
```

## Cloning

#### Duplicate a Table Schema

```sql
create table emp_dup like employee;
```

#### Duplicate a Table

```sql
create table emp_dup select * from employee;
```

## Access Controls

#### Creating New User

```sql
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```

the hostname part is set to `localhost`, so the user will be able to connect to the MySQL server only from the localhost.  
To grant access from another host, change the hostname part with the remote machine IP.

```sql
CREATE USER 'username'@'172.8.10.5' IDENTIFIED BY 'user_password';
```

To create a user that can connect from any host, '%' is used in the hostname part:

```sql
CREATE USER 'username'@'%' IDENTIFIED BY 'user_password';
```

#### Grant All Permissions

```sql
GRANT ALL PRIVILEGES ON * . * TO 'username'@'localhost';
```

Asterisks(\*) refers to the database and table names respectively.  
By using asterisks we can give access of all the databases **or** tables to the user.

#### Flush Privileges

```sql
FLUSH PRIVILEGES
```

All the changes won't be in effect unless this query is fired.

#### Specific User Permissions

```sql
GRANT type_of_permission ON database_name.table_name TO 'username'@'localhost';
```

`type_of_permission` may have one of these value:

- **ALL PRIVILEGES** - Allows user full access to a designated database (or if no database is selected, global access across the system).
- **CREATE** - allows them to create new tables or databases.
- **DROP** - allows them to them to delete tables or databases.
- **DELETE** - allows them to delete rows from tables.
- **INSERT** - allows them to insert rows into tables.
- **SELECT** - allows them to use the `SELECT` command to read through databases.
- **UPDATE** - allow them to update table rows.
- **GRANT OPTION** - allows them to grant or remove other users’ privileges.  
  Multiple permissions are given with commas.

#### Revoking permissions

```sql
REVOKE type_of_permission ON database_name.table_name FROM 'username'@'localhost';
```

#### Show User's Current Permissions

```sql
SHOW GRANTS FOR 'username'@'localhost';
```

#### Delete a User

```sql
DROP USER 'username'@'localhost';
```

#### Set new password to a user

```sql
use mysql;
update user set authentication_string=PASSWORD("<new2-password>") where User='<user>';
flush privileges;
```

## Reset Root Password

Stop MySQL service

```
sudo systemctl stop mysql
```

Restart MySQL service without loading grant tables

```bash
sudo mysqld_safe --skip-grant-tables &
```

The apersand (&) will cause the program to run in the background and `--skip-grant-tables` enables everyone to to connect to the database server without a password and with all privileges granted.
Login to shell

```
mysql -u root
```

Set new password for root

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'MY_NEW_PASSWORD';
FLUSH PRIVILEGES;
```

Stop and start the server once again

```
mysqladmin -u root -p shutdown
sudo systemctl start mysql
```

## Programming

#### Declare variables

```sql
set @num = 10;
set @name = 'Anurag';
```

#### Print them

```sql
select @name;
```

#### For loop

```sql
set @n = 21;
select repeat("* ", @n := @n - 1) from information_schema.tables where @n > 0;
```

## Miscellaneous

#### Round

```sql
select round(3.141596, 3);
```

#### Repeated concatenation

```sql
select repeat("* ", 20);
```

#### Random float

```sql
select rand();
```

#### Typecast to Int

```sql
select cast(23.01245 as signed);
```

#### Concatenation

```sql
select concat("Mahesh", " ", "Chandra", " ", "Duddu", "!");
```

#### Extract Month

```sql
select month("1998-12-30");
```

#### Extract Year

```sql
select year("1998-12-30");
```
