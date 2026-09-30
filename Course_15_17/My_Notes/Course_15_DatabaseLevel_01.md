This course helps you save development time.  
  
---  
# Introduction  
## What is Database?  
Row = Entity = Record. They all refer to a row in a table.  
Column = Field = Attribute. They all refer to a column in a table.  
Table = Entity set.  
  
## What is NULL?  
NULL is a special value.  
You can decide whether a field in a table accepts NULL values or not.  
When the field in a table accepts NULL values, it means the field is optional.  
NULL usage : the value is missing - the value is optional - we don't know the value yet.  
  
> NULL can affect the results of queries and calculations in unexpected ways.  
  
## Primary key vs Foreign key  
Primary key: no duplications, means it must be unique - NULLs are not allowed - should not be changed.  
A primary key can be two fields. But the good practice is to choose one field to be the primary key.  
  
It is better for the primary key to be a number, not text. Because text takes time to execute, and takes additional space.  
Suppose that the primary key is "Faculty of science". You need to **_duplicate_** that in other tables to refer to this! this takes space. Also, searching for numbers is faster than searching for strings.  
  
Foreign key is a primary key in another table.  
> Foreign key establishes a relationship between two tables, allowing data to be shared and linked between them.  
  
Foreign key means there is a relationship between two tables.  
  
The primary key should not change, because it has things depend on it.  
  
Data integration problem /  Referential integrity problem: for example when you reference the primary key of a row that does not exist.  
Or when you delete a row, that has rows in other tables depend on it.  
  
Cascade delete : delete the row in this table and delete all rows in other tables that depend on this row.  
Do not use the cascade delete, or be careful.  
  
RDBMS help you design/develop databases in a good way, it prevent you from facing some problems. Files don't help you achieve that.  
  
## Redundancy  
Means there are duplicated data in the database.  
  
Redundancy is a cause for other problems.  
Normalization is a solution for the redundancy problem. For example, breaking down a table into two separated tables that has relationship between them is a normalization technique.  
There are many normalization techniques.  
  
Redundancy is not always bad. For example you can put a field in a table that stores the number of specific records in another table. Here you don't need to store this information, you can counts the records wherever you want. But storing it, saves time.  
  
## Data Integrity  
Reliable means I can trust it.  
  
Types of data integrity:  
- Entity integrity: each row in a table can uniquely identified. Achieved using primary keys.  
- Referential integrity: achieved using foreign keys.  
- Domain integrity: the value is between the specified range of values. For examples: valid dates - valid numbers (-400$ as salary is wrong).  
- Business integrity: for example, the requirements of a bank system might given that to create an account, the min balance must be 500$. So you should meet that in the database.  
  
Data integrity is important. Without it, organizations risk making decisions based on inaccurate data, which can lead to poor outcomes.  
  
To maintain data integrity, we use Constraints.  
  
> Data integrity refers to the accuracy, consistency, and reliability of data over its entire life cycle, from creation to deletion.  
  
## Constraints  
They are rules or conditions that we apply on data to ensure its integrity and consistency.  
Can be applied on one field or the entire table.  
  
Common types of constraints in databases  
- Primary key constraint.  
- Foreign key constraint.  
- Unique constraint.  
- Not null constraint.  
- Check constraint. The data should meet a specific condition you write.  
  
Primary key constraint doesn't allow null while the unique constraint does.  
  
## SQL  
We use SQL to communicate with a database. It lets you access and manipulate databases.  
  
Types of SQL statements:  
- Data Definition Language (DDL). Example: create - drop -alter - truncate.  
- Data Manipulation Language (DML). Example: insert - update - delete.  
- Data Control Language (DCL). Example: grant - revoke.  
- Transaction Control Language (TCL). Example: commit - rollback - savepoint.  
- Data Query Language (DQL). Example: select.  
  
In files, one user can access the data at a time. In DBMSs, multiple users can access at the same time.  
  
In files, when you need something, you load all records into the ram.  
Using a database engine, you don't.  
  
---  
# Conceptual Design  
## ER Diagram  
The ER diagram depends on: entities - relations - attributes.  
These are the main things in any ER diagram.  
  
> ER diagram reduces complexity and allows database designers to build databases quickly.  
  
> ER Diagram is a structural design of the database. It is a conceptual design. It is not a physical design.  
  
## ER Diagram Symbols  
Strong entity = rectangle. It is strong because it has a primary key.  
Weak entity = rectangle inside another rectangle. It is weak because it doesn't have a primary key.  
  
## Components of ER diagram  
Entities  
- Entity (strong entity).  
- Weak entity.  
Attributes  
- Attribute.  
- Key attribute.  
- Composite attribute.  
- Multivalued attribute.  
- Derived attribute.  
Relationships  
- One-to-One Relationship.  
- One-to-Many Relationship.  
- Many-to-One Relationship.  
- Many-to-Many Relationship.  
  
## Strong & Weak entity  
You achieve the "entity integrity" by having only strong entities.  
  
![[Pasted image 20260803013521.png|780]]  
The "relation" here is: son - daughter - etc.  
This is an Employee and their children.  
  
## Attributes  
The key attribute is underlined. It uniquely identifies the entity in the entity set.  
Derived attribute means that the value of this attribute can be concluded from another attribute. Represented as dashed circle.  
Multivalued attribute is an attribute that stores multiple values. This is a bad practice. Represented as a circle inside another circle.  
Composite attribute, like, name: first - mid - last.  
  
## Relationships  
You can have many relationships between two entities.  
![[Pasted image 20260803031412.png|658]]  
  
This is self referencing relationship.  
![[Pasted image 20260803031738.png]]  
![[Pasted image 20260803031808.png]]  
  
## Cardinality vs Ordinality  
Cardinality -> max.  
Ordinality -> min.  
  
`(x,y)` x is the ordinality, and y is the cardinality. (Not very sure about this idea).  
![[Pasted image 20260804171418.png|876]]  
Using the ordinality we specify if it is optional/mandatory to relate to an instance of another entity or not.  
  
## Cardinality symbols  
![[Pasted image 20260804181324.png|477]]  
  
## Process of creating ER diagram  
Steps to create ERD:  
1. Entity Identification.  
2. Relationship Identification. Among all entities.  
3. Cardinality Identification. In each relationship.  
4. Identity Attributes.  
5. Create ERD.  
6. Look for Generalizations and edit if any.  
  
Exercise:  
![[Pasted image 20260804193853.png|776]]  
  
1 - Entities  
![[Pasted image 20260804194052.png|365]]  
  
2 - Relationships  
![[Pasted image 20260804194530.png|491]]  
  
3 - Cardinalities  
![[Pasted image 20260804213741.png|557]]  
  
4 - Attributes  
![[Pasted image 20260804215822.png|707]]  
  
You can use erdplus.com to draw diagrams.  
  
## Associative Entities  
![[Pasted image 20260804234127.png|437]]  
Means: the result of the relationship between Student and Course has a relationship with Teacher.  
It is "Associative Entity" because it is mainly a relationship.  
When we talk about "Associative Entity" then we are talking about a many-to-many relationship.  
  
## Generalization  
![[Pasted image 20260805003525.png|538]]  
Extract the common attributes and put them in a generalized entity.  
Bottom-Up approach. Converting to a thing more generic. From a known thing to an unknown thing.  
  
## Specialization  
![[Pasted image 20260805030310.png|542]]  
Top-Down approach.  
> A higher-level entity is divided into multiple specialized lower-level entities.  
  
---  
# Relational Schema  
Tables with relationships between them.  
  
## Convert self referential to relational schema  
![[Pasted image 20260805042224.png|603]]  
  
> In the same table we add a foreign key field to the primary key of the row.  
  
You can read it like this:  
- A `ManagerID` may appear in 0 or 1 row in the `ID` field.  
- An `ID` may appear in 0 or M rows in the `ManagerID` field.  
  
## Convert Composite-Multivalued-Derived attributes to relational schema  
Each field in any table should represent one thing.  
  
The entity is `student`.  
The relational schema is `student`.  
The database table is `students`.  
  
![[Pasted image 20260805221628.png|579]]  
We remove the derived attribute.  
  
Steps:   
1. Create table for the entity.  
2. Move attributes to that table.  
3. Composite attributes: only take roots.  
4. Derived attributes will be ignored.  
5. We create new table for each multivalued attribute.  
6. We take the primary key from the main entity and put it in the new one as FK (for the multivalued attribute).  
  
## One-to-one to relational schema  
![[Pasted image 20260806003424.png|656]]  
  
Steps:  
1. We create a table for each entity with it's attributes.  
2. We take the primary key from any side and put it in the other side.  
  
## One-to-many && many-to-one to relational schema  
![[Pasted image 20260806012722.png|665]]  
  
Steps:  
1. We create a table for each entity with it's attributes.  
2. We take the primary key from the "one" side and put it as foreign key in the "many" side.  
  
Put any attributes that relate to the relationship in the "many" side.  
  
## Many-to-many to relational schema  
![[Pasted image 20260806022753.png|793]]  
  
Steps:  
1. We create a table for each entity with it's attributes.  
2. Create a bridge table for the many to many relationship.  
3. Take the primary keys from both tables and put them in the bridge table.  
4. Add the primary key to the bridge table.  
5. Add any attributes related to the relationship to the bridge table.  
  
## Generalization and Specialization to relational schema  
![[Pasted image 20260806032228.png|564]]  
The relationship is always one-to-one.  
> You take the primary key from the parent entity and put it as foreign key in the child entity.  
  
## Associative entity to relational schema  
![[Pasted image 20260806034525.png|637]]  
  
Steps:  
1. We create a table for each entity with it's attributes.  
2. Create a bridge table for the many to many relationship.  
3. Take the primary keys from the 3 entities you have and put them in the bridge table.  
  
---  
# SQL - DDL  
## Create Database  
There is a button to execute the commands, and a button to check the syntax.  
You can have as many databases as you want.  
```sql  
create database 'koko';  
```  
  
## Create a database if not exists  
```sql  
-- to select all databases  
select * from sys.databases where name = 'koko';  
  
-- to create the database if it doesn't exist  
-- so you don't get an error  
if not exists(select * from sys.databases where name = 'koko')  
	begin  
		create database koko;  
	end  
```  
  
## Switch database  
```sql  
USE <database_name>;  
```  
  
## Drop database  
```sql  
drop database <database_name>;  
```  
  
## Drop database if exists  
```sql  
if exists(select * from sys.databases where name = 'koko')  
	begin  
		drop database koko;  
	end  
```  
  
## Create table  
  
For ID, we usually use the datatype `int`.  
For strings, you can use:  
- `char(length)` this allocates `length` English spaces.  
- `nchar(length)` this allocates `length` Unicode spaces.  
- `varchar(length)` this allocates English spaces based on the length of the word entered.  
- `nvarchar(length)` this allocates Unicode spaces based on the length of the word entered.  
  
We usually use `nvarchar(length)`.  
  
```sql  
use koko;  
create table Employees (  
	ID int not null,  
	Name nvarchar(50) not null,  
	Phone nvarchar(10) null,  
	Salary smallmoney null,  
	primary key (ID)  
);  
```  
  
## SQL Datatypes  
![[Pasted image 20260807041341.png|573]]  
  
Use `nvarchar(max) varchar(max) varbinary(max)` data types instead of `ntext text image` because SQL server will remove them in the future versions.  
  
### Exact numeric datatypes  
  
Decimal and numeric are synonyms.  
  
The number you store is the number you get.  
There is no hidden binary approximation.  
  
![[Pasted image 20260807045103.png|564]]  
  
### Approximate numeric datatypes  
For scientific calculations.  
![[Pasted image 20260807045255.png|564]]  
  
### Character strings datatypes  
> The text data type can store non-Unicode data in the code page of the server. Means, it can't store "ياسين", for example.  
  
![[Pasted image 20260807050334.png|567]]  
  
### Unicode character string datatypes  
![[Pasted image 20260807050443.png|549]]  
  
### Date & Time datatypes  
Use the ones in blue.  
![[Pasted image 20260807054949.png|552]]  
  
### Binary string datatypes  
![[Pasted image 20260807055108.png|539]]  
  
> Storing large videos puts a heavy load on SQL Server, which is optimized for managing data rather than serving large media files.  
  
Store large files on the file system - cloud storage - server and store the url in sql server.  
  
### Other datatypes  
![[Pasted image 20260807060713.png|520]]  
  
## Drop table  
```sql  
drop table <table_name>;  
```  
  
---  
# SQL - DDL - Alter table statement  
  
## Add column  
```sql  
alter table <table_name>  
add <column_name> char(1);  
```  
  
## Rename column  
Most database engines share almost the same sql syntax.  
```sql  
alter table employees  
RENAME column genderr to gender;  
  
-- for sql server use this  
-- this is a stored procedure, consider it as pre-written function ready for usage  
exec sp_rename 'employees.genderr', 'gender', 'column';  
exec sp_rename '<table_name>.<old_column_name>', 'new_column_name', 'column';  
  
-- Microsoft recommends that you drop and recreate the table.  
```  
  
## Rename a table  
```sql  
alter table <old_table_name>  
rename to <new_table_name>;  
  
-- for sql server, use this  
exec sp_rename 'employees', 'emps';  
  
-- Microsoft recommends that you drop and recreate the table.  
```  
  
## Modify a column  
```sql  
-- for sql server and PostgreSql  
alter table emps  
alter column Name nvarchar(100) not null;  
  
-- removing "not null" makes it null  
alter table emps  
alter column Name nvarchar(100);  
  
-- for Mysql  
alter table emps  
modify column Name nvarchar(100);  
  
-- for Oracle  
alter table emps  
modify Name nvarchar(100);  
```  
  
## Delete a column  
```sql  
alter table emps  
drop column salary;  
```  
  
---  
# Backup and restore database  
## Backup database  
In this way, you are backing up the full database.  
Note that you should make the back up to a different driver, not the same driver the real database on.  
  
Using mouse  
- Right click on the database  
- Tasks  
- Back up  
- Choose the location and the name  
- Common convention: for database backups we use the extension `.bak` as `name.bak`  
  
The script  
```sql  
backup database koko  
to disk = 'd:\x\kokoo.bak';  
```  
  
## Differential Backup  
```c  
// suppose that you have a backup that has  
A - B - C - D  
// and your current database has  
A - B - C - D - E - F  
// then the differential backup will upload only  
E - F  
// and the result will be  
A - B - C - D - E - F  
```  
  
Syntax  
```sql  
backup database koko  
to disk = 'd:\x\koko.bak'  
with differential;  
```  
  
Full backups take time and space.  
  
## Restore Database  
  
Script  
```sql  
-- choose the master database  
restore database koko  
from disk = 'd:\x\koko.bak';  
```  
I guess there are stuff here you need to search about.  
  
---  
# Data Manipulation Language DML  
## Insert Into statement  
  
Script  
```sql  
-- this inserts one record  
-- if you don't want to specify the column names, make sure that the order of the values is correct.  
insert into emps  
values  
(1, 'Yasin Hamad', 1111, 1000);  
  
-- this inserts multiple records  
insert into emps  
values  
(2, 'Yasin Hamad', 1111, 1000),  
(3, 'Yasin Hamad', 1111, 1000),  
(4, 'Yasin Hamad', 1111, 1000),  
(5, 'Yasin Hamad', 1111, 1000);  
  
-- this inserts a record with only these data  
insert into emps (id, name)  
values  
(7, 'yasin hamad');  
  
-- you can use "null" if the column allows that  
insert into emps  
values  
(12, 'Yasin Hamad', null, null);  
  
-- this deletes all records that are in the table  
delete from emps;  
```  
  
Note  
```sql  
-- notice that these are TWO statements  
-- if you run them together, 2 records will be effected  
-- the second statemnet will fail, becase the PK "1" exists in the table  
-- notice that the first record in the second statement, PK "3", will not be inserted, becaue the statement failed.  
insert into emps  
values  
(1, 'Yasin Hamad', 1111, 1111),  
(2, 'Yasin Hamad', 1111, 1000);  
  
insert into emps  
values  
(3, 'Yasin Hamad', 1111, 1111),  
(1, 'Yasin Hamad', 1111, 1000);  
```  
  
Note that you can add records using mouse.  
  
## Update Statement  
  
Script  
```sql  
-- if you run this statement without the where condition, then, all records will have this name and age  
update emps  
set name = 'Yasin Hamad', age = 24  
where id = 1;  
  
-- you can type the condition you want  
update emps  
set age = age + 1  
where age <= 24;  
```  
  
## Delete Statement  
  
Script  
```sql  
-- you can type the condition you want  
delete from emps  
where age is null; -- you can use "is null"  
delete from emps  
where age is not null; -- you can use "is not null"  
  
-- this deletes all records  
delete from emps;  
  
-- another example  
delete from emps  
where id = 1;  
```  
  
## Select Into Statement  
  
Script  
```sql  
-- collect the data - create the new table - insert the data into the new table  
-- the new table will be created as follows  
	-- the columns are identified using the select statement  
	-- the signature of each column will be similar to the original table (I noticed that it doesn't specify the primary key field)  
-- if the new table you want to create and insert the data into exists, you'll get an error  
select *  
into empsCopy1  
from emps;  
  
-- with only id, and name columns  
select id, name  
into empsCopy2  
from emps;  
  
-- this is a trick to create an empty copy of a table  
select *  
into empsCopy3  
from emps  
where 5=6;  
```  
  
## Insert Into Select From Statement  
  
Script  
```sql  
-- if empsCopy doesn't exist, you'll get an error  
-- we use this to copy records from table to another existing table  
-- in order to be able to run this, the column names in the two tables must match  
-- if you want to copy the data to a table that doesn't exist in the database, you can use "select into" instead  
insert into empsCopy  
select * from emps;  
  
-- you can specify the conditions you want  
insert into empsCopy  
select * from emps  
where age >= 30;  
```  
  
---  
# Misc 1  
## Identity Field - Auto Increment  
  
Script  
```sql  
CREATE TABLE deps (  
   -- the first 1 is the seed, that mean it'll start from number 1  
   -- the second 1 is the increment number, which means it'll increment the number by one each time "1 2 3"  
   ID int IDENTITY(1,1) PRIMARY KEY,  
   Name varchar(255) NOT NULL,  
);  
  
-- when you insert, you don't specify the id  
insert into deps  
values  
('Marketing');  
  
-- after inserting a record, Sql puts the id in this variable  
insert into deps  
values  
('IT');  
print @@identity;  
```  
  
## Delete vs Truncate  
  
```sql  
-- you can't use "where" with truncate  
-- it deletes all records  
-- it resets the auto number, where as the "delete" statement doesn't reset it  
-- the delete statement deletes the records one by one, where as truncate doesn't (it deallocates the data pages)  
truncate table deps;  
  
-- truncate is faster than delete  
delete from deps;  
```  
  
## Foreign Key Constraint  
  
Script  
```sql  
-- This table doesn't have foreign keys, so create it first  
create table Customers (  
  ID int ,  
  FirstName varchar(40),  
  LastName varchar(40),  
  Age int,  
  Country varchar(10),  
  primary key (id)  
);  
  
-- Adding foreign key to the CustomerID field  
-- The foreign key references to the ID field of the Customers table  
create table Orders (  
  OrderID int,  
  Item varchar(40),  
  Amount int,  
  CustomerID int references customers(ID), -- this is the foreign key  
  primary key (OrderID)  
);  
```  
  
You can add a foreign key using alter, in this way  
```sql  
alter table orders  
add foreign key (CustomerID) references customers(ID);  
```  
  
You can design a query using the mouse. Open a new file "new query" - right click on the screen - choose "design query in editor".  
  
When creating tables, first, create the tables that don't have foreign keys.  
When deleting tables, first, delete the tables that have foreign keys.  
  
You can set the foreign key using the mouse.  
Right click on the table that has the foreign key - choose "Design" - right click on the row - choose "Relationships".  
  
---  
# Data Query Language - DQL - SQL Queries  
  
If you have a problem viewing the diagrams, run this  
```sql  
EXEC sp_changedbowner 'sa';  
```  
  
You can view the database tables as diagrams, under Database diagrams, Right click on it and choose "new database diagram".  
  
## Select Statement  
  
When you run this, you get a result, this result is stored in a table, and it is called the result-set.  
```sql  
-- * means all columns  
-- these two statements are similar  
select * from employees;  
select employees.* from employees;  
  
-- you can specify the columns  
select id, firstname, lastname, MonthlySalary from employees;  
```  
  
## Select Distinct Statement  
  
Script  
```sql  
-- you will not get two similar rows - no repetition - no two similar rows  
select departmentid from Employees;  
select distinct departmentid from Employees  
  
select FirstName from Employees;  
select distinct FirstName from Employees  
  
-- you can get two rows like this, because the two rows are not similar  
	-- Yasin Hamad, 1  
	-- Yasin Hamad, 2  
-- or  
	-- Ahmad Hasan, 1  
	-- Yasin Hamad, 1  
select FirstName, DepartmentID from Employees;  
select distinct FirstName, DepartmentID from Employees  
```  
  
## Where Statement - And - Or - Not  
  
The "where" statement filters the rows. Here, you can type conditions similar to the ones you type in any IF statement in programming languages.  
Don't forget that you can type complex condition in order to get from the database what you want. `(- and -) or not (- or -)`  
  
Script  
```sql  
-- I noticed that you can type 'm' and 'M', they are similar  
select * from employees  
where gendor = 'm';  
  
select * from employees  
where MonthlySalary <= 500;  
-- you can nigate the condition in this way using "not"  
select * from employees  
where not MonthlySalary <= 500;  
-- or  
select * from employees  
where MonthlySalary > 500;  
  
-- you can use "and" and "or"  
select * from employees  
where MonthlySalary > 500 and gendor = 'm';  
  
-- this is the !=  
select * from employees  
where CountryID <> 1;  
  
select * from employees  
where ExitDate is null;  
-- you can nigate it in this way  
select * from employees  
where ExitDate is not null;  
```  
  
## "In" Operator  
This operator is important.  
  
Script  
```sql  
-- instead of this  
select * from employees  
where DepartmentID = 1 or DepartmentID = 2 or DepartmentID = 3;  
-- you can use  
select * from employees  
where DepartmentID in (1,2,3);  
  
-- firstname and the values in the () should be of the same type  
select * from Employees  
where FirstName in ('kai', 'robert', 'jade');  
  
-- these are the department IDs that have employees that take salaries <=210  
select Employees.DepartmentID from Employees where MonthlySalary <= 210;  
-- you can get the department names in this way  
select Departments.Name from Departments   
where ID in (select Employees.DepartmentID from Employees where MonthlySalary <= 210);  
-- you can negate it in this way using the "not"  
select Departments.Name from Departments   
where ID not in (select Employees.DepartmentID from Employees where MonthlySalary <= 210);  
  
-- note that you can also put one value  
select * from Employees  
where FirstName in ('kai');  
```  
  
## Sorting: Order by  
  
Script  
```sql  
-- by default it is asc  
select ID, FirstName, MonthlySalary from Employees  
where DepartmentID = 1  
order by FirstName;  
-- so it is similar to   
select ID, FirstName, MonthlySalary from Employees  
where DepartmentID = 1  
order by FirstName asc;  
-- you can set it to desc in this way  
select ID, FirstName, MonthlySalary from Employees  
where DepartmentID = 1  
order by FirstName desc;  
  
-- you can order the result according to two fields  
select ID, FirstName, MonthlySalary from Employees  
where DepartmentID = 1  
order by FirstName, MonthlySalary;  
-- it is "asc" by default, so, the above statement is similar to  
select ID, FirstName, MonthlySalary from Employees  
where DepartmentID = 1  
order by FirstName asc, MonthlySalary asc;  
-- you get  
	-- Adam, 576.00  
	-- Adam, 856.00  
-- but, using this  
select ID, FirstName, MonthlySalary from Employees  
where DepartmentID = 1  
order by FirstName asc, MonthlySalary desc;  
-- you get  
	-- Adam, 856.00  
	-- Adam, 576.00  
	  
-- without "order by", you get the result-set as it is sorted  
-- "asc" means from 1 to 9, means from a to z. "desc" is the inverse  
```  
  
## Select Top Statement  
  
Don't forget that you can build the query step by step and see the results. Until you get what you want.  
You are free to do that in management studio, you don't have to write the big query in one shot.  
  
Script  
```sql  
-- this retrieves the top 5 records  
-- don't forget that "*" means: all columns  
select top 5 * from Employees;  
-- you can specify the columns  
select top 5 id, FirstName, LastName from Employees;  
  
-- Question:  
-- Retrieve the employee names that takes the bigger 5 salaries  
  
-- these are the whole salaries descendingly  
select distinct Employees.MonthlySalary from Employees  
order by MonthlySalary desc;  
  
-- these are the top 5 salaries from the above statement  
select distinct top 5 Employees.MonthlySalary from Employees  
order by MonthlySalary desc;  
  
-- these are the employees that take these salaries  
select Employees.ID, Employees.FirstName, Employees.MonthlySalary from Employees  
where MonthlySalary in  
(  
	select distinct top 5 Employees.MonthlySalary from Employees  
	order by MonthlySalary desc  
);  
  
-- we can order the result  
select Employees.ID, Employees.FirstName, Employees.MonthlySalary from Employees  
where MonthlySalary in  
(  
	select distinct top 5 Employees.MonthlySalary from Employees  
	order by MonthlySalary desc  
)  
order by MonthlySalary desc;  
```  
  
```sql  
-- this doesn't retrieve the top 10  
-- if you have 1000 records, you'll see the top 100  
select top 10 percent * from Employees;  
```  
  
## Select As  
  
```sql  
-- you can create columns  
select A = 3*2, B = 9/2.0;  
  
-- this is a system function, it returns the current system date  
select GetDate();  
select Today = GetDate();  
select GetDate() as Today;  
  
-- it does the same operation for each record  
select A = 3*2, B = 9/2.0  
from Employees;  
  
-- you can use fields from the table itself  
select MonthlySalary, YearlySalary = MonthlySalary * 12  
from Employees;  
  
select FullName = FirstName + ' ' + LastName, YearlySalary = MonthlySalary * 12  
from Employees;  
-- you can also write the above statement in this way  
select FirstName + ' ' + LastName as FullName, YearlySalary = MonthlySalary * 12  
from Employees;  
  
select FirstName, BonusPerc, MonthlySalary, BonusAmoutn = MonthlySalary * BonusPerc  
from Employees  
  
-- DATEDIFF() is a system function.  
-- YEAR means, return the difference in years, you can change that.  
select FirstName + ' ' + LastName as FullName, Age = DATEDIFF(YEAR, employees.DateOfBirth, GetDate())  
from Employees  
order by FullName;  
  
-- You can   
	-- Add calculated fields - new columns, in which you can use the columns of the table itself, functions, and expressions  
	-- Compine existing columns.  
	-- Use system functions  
	-- Use your own functions  
```  
  
## Between Operator  
  
```sql  
-- they are similar  
-- the second way is shorter  
select * from Employees  
where MonthlySalary >= 500 and MonthlySalary <= 1000;  
  
select * from Employees  
where MonthlySalary between 500 and 1000;  
  
-- note that you can use between with dates  
```  
  
## Count, Sum, Avg, Min, Max functions  
  
```sql  
-- use the function with a table  
-- you have the function, and you give it a table to work on  
select  
	TotalCount = count(MonthlySalary),  
	TotalSum = sum(MonthlySalary),  
	Average = avg(MonthlySalary),  
	MaxSalary = max(MonthlySalary),  
	MinSalary = min(MonthlySalary)  
from Employees;  
  
-- you can use where  
select  
	TotalCount = count(MonthlySalary),  
	TotalSum = sum(MonthlySalary),  
	Average = avg(MonthlySalary),  
	MaxSalary = max(MonthlySalary),  
	MinSalary = min(MonthlySalary)  
from Employees  
where DepartmentID = 3;  
  
select TotalEmployees = count(id) from Employees; -- 1000  
-- if the value is null, the function "count" doesn't count it  
select ResignedEmployees = count(ExitDate) from Employees; -- 103  
```  
  
## Group By  
  
```sql  
-- group by DepartmentID, means calculate the results per DepartmentID  
select  
	TotalCount = count(MonthlySalary),  
	TotalSum = sum(MonthlySalary),  
	Average = avg(MonthlySalary),  
	MaxSalary = max(MonthlySalary),  
	MinSalary = min(MonthlySalary)  
from Employees  
group by DepartmentID;  
  
-- you can show the departments  
select  
	Employees.DepartmentID,  
	TotalCount = count(MonthlySalary),  
	TotalSum = sum(MonthlySalary),  
	Average = avg(MonthlySalary),  
	MaxSalary = max(MonthlySalary),  
	MinSalary = min(MonthlySalary)  
from Employees  
group by DepartmentID;  
  
-- you can order them  
select  
	Employees.DepartmentID,  
	TotalCount = count(MonthlySalary),  
	TotalSum = sum(MonthlySalary),  
	Average = avg(MonthlySalary),  
	MaxSalary = max(MonthlySalary),  
	MinSalary = min(MonthlySalary)  
from Employees  
group by DepartmentID  
order by DepartmentID;  
  
select  
	TotalCount = count(MonthlySalary),  
	TotalSum = sum(MonthlySalary),  
	Average = avg(MonthlySalary),  
	MaxSalary = max(MonthlySalary),  
	MinSalary = min(MonthlySalary)  
from Employees  
group by DepartmentID  
order by TotalCount;  
  
-- the main idea here is that, you can use the functions "sum avg max min count"  
-- but "group by" helps you maximize their output  
-- how? by making them do the same job per specific value/column you specify  
```  
  
## Having  
  
```sql  
-- "having" is related to "group by"  
-- "having" is similar to "where" in normal queries, it process over the result of "group by"  
-- "having" is a filter for "group by", similar to "where" that is a filter for normal queries  
select  
	Employees.DepartmentID,  
	TotalCount = count(MonthlySalary),  
	TotalSum = sum(MonthlySalary),  
	Average = avg(MonthlySalary),  
	MaxSalary = max(MonthlySalary),  
	MinSalary = min(MonthlySalary)  
from Employees  
group by DepartmentID  
having count(MonthlySalary) > 100  
order by DepartmentID;  
  
-- you can use "where" with "group by" in this way  
select * from (  
	select  
		Employees.DepartmentID,  
		TotalCount = count(MonthlySalary),  
		TotalSum = sum(MonthlySalary),  
		Average = avg(MonthlySalary),  
		MaxSalary = max(MonthlySalary),  
		MinSalary = min(MonthlySalary)  
	from Employees  
	group by DepartmentID  
) as R1  
where R1.TotalCount > 100  
order by R1.DepartmentID;  
```  
  
## Like  
  
```sql  
--Finds any values that start with "a"  
select ID, FirstName from Employees  
where FirstName like 'a%';  
  
--Finds any values that end with "a"  
select ID, FirstName from Employees  
where FirstName like '%a';  
  
--Finds any values that have "tell" in any position  
select ID, FirstName from Employees  
where FirstName like '%tell%';  
  
--	Finds any values that start with "a" and ends with "a"  
select ID, FirstName from Employees  
where FirstName like 'a%a';  
  
--Finds any values that have "a" in the second position  
select ID, FirstName from Employees  
where FirstName like '_a%';  
  
--Finds any values that have "a" in the third position  
select ID, FirstName from Employees  
where FirstName like '__a%';  
  
--Finds any values that start with "a" and are at least 3 characters in length  
select ID, FirstName from Employees  
where FirstName like 'a__%';  
  
--Finds any values that start with "a" and are at least 4 characters in length  
select ID, FirstName from Employees  
where FirstName like 'a___%';  
  
--Finds any values that start with "a" or "b"  
select ID, FirstName from Employees  
where FirstName like 'a%' or FirstName like 'b%';  
  
-- "%" represents zero, one, or more chars  
-- "_" represents one, single char.  
  
-- for MS access we use "*" instead of "%" and "?" instead of "_"  
  
-- we use "like" in the "where" clause  
```  
  
## WildCards  
  
```sql  
select ID, FirstName, LastName from Employees  
Where firstName = 'Mohammed' or FirstName ='Mohammad';   
-- will search for Mohammed or Mohammad  
select ID, FirstName, LastName from Employees  
Where firstName like 'Mohamm[ae]d';  
  
--You can use Not   
select ID, FirstName, LastName from Employees  
Where firstName Not like 'Mohamm[ae]d';  
  
select ID, FirstName, LastName from Employees  
Where firstName like 'a%' or firstName like 'b%' or firstName like 'c%';  
-- search for all employees that their first name start with a or b or c  
select ID, FirstName, LastName from Employees  
Where firstName like '[abc]%';  
  
-- search for all employees that their first name start with any letter from a to l  
select ID, FirstName, LastName from Employees  
Where firstName like '[a-l]%';  
  
-- h[^oa]t finds "hit", but not "hot" and "hat"  
```  
  
---  
# Joins  
## Inner Join  
  
```sql  
select Customers.CustomerID, Customers.Name, Orders.OrderID, Orders.Amount  
from Customers   
inner join Orders   
on Customers.CustomerID = Orders.CustomerID;  
-- similar to  
select Customers.CustomerID, Customers.Name, Orders.OrderID, Orders.Amount  
from Customers   
join Orders   
on Customers.CustomerID = Orders.CustomerID;  
```  
  
```sql  
-- I build all queries here using query designer  
-- note that you can select the query you built and hit "design query in editor" to edit it  
  
-- Be careful, whey you open the query designer, the order of choosing the tables change the final query  
  
SELECT Employees.ID, Employees.FirstName, Employees.LastName, Departments.Name as DepartmentName  
FROM Employees INNER JOIN  
Departments ON Employees.DepartmentID = Departments.ID  
  
-- you can use "where"  
SELECT Employees.ID, Employees.FirstName, Employees.LastName, Departments.Name as DepartmentName  
FROM Employees INNER JOIN  
Departments ON Employees.DepartmentID = Departments.ID  
where Departments.ID = 1;  
  
-- these are three tables  
-- it is easy to built them using the query designer  
SELECT Employees.ID, Employees.FirstName, Employees.LastName, Countries.Name AS CountryName, Departments.Name AS DepartmentName  
FROM Employees INNER JOIN  
Countries ON Employees.CountryID = Countries.ID INNER JOIN  
Departments ON Employees.DepartmentID = Departments.ID;  
```  
  
## Left Join  
  
```sql  
  
-- first, choose all records from the left table, then start adding the matching records from the right table  
-- to to choose "left outer join" in query designer: right click on the relation that is between the tables and choose what you want  
  
select Customers.CustomerID, Customers.Name, Orders.OrderID, Orders.Amount  
from Customers   
left join Orders   
on Customers.CustomerID = Orders.CustomerID;  
-- similar to  
select Customers.CustomerID, Customers.Name, Orders.OrderID, Orders.Amount  
from Customers   
left outer join Orders   
on Customers.CustomerID = Orders.CustomerID;  
```  
  
## Right Join and Full Join  
  
```sql  
-- right join = right outer join  
-- full join = full outer join  
  
select Customers.CustomerID, Customers.Name, Orders.OrderID, Orders.Amount  
from Customers   
right join Orders   
on Customers.CustomerID = Orders.CustomerID;  
  
select Customers.CustomerID, Customers.Name, Orders.OrderID, Orders.Amount  
from Customers   
full join Orders   
on Customers.CustomerID = Orders.CustomerID;  
  
-- the inner join is the one you'll most use  
```  
  
---  
# Views  
  
```sql  
-- you create a view x using a query y  
-- whenever you use the view x to execute a query z, the database engine first executes the query y then executes the query z based on the result-set/table of y  
-- we call the view x a virtuall table because, whenever you execute a query, the database engine executes the query of the view x first and get the table we want to work on, but it is not a real table  
-- use cases for views:  
	-- you have a sample of data you use a lot, so, when you create a view for it, you save time, because, now, you don't keep typing the same piece of query  
	-- instead of giving users full access to a table, you can create a view with the fields you want them to access, then give them access to the view, this is for security  
-- view = select statement, this statement may be 10 pages for example! this is normal  
-- views always show up-to-date data.  
  
create view ActiveEmployees as  
select * from Employees  
where ExitDate is null;  
  
create view ResignedEmployees as  
select * from Employees  
where ExitDate is not null;  
  
select * from ActiveEmployees;  
select * from ResignedEmployees;  
-- the above two statements are similar to   
select * from  
(  
select * from Employees  
where ExitDate is null  
) as R1;  
  
select * from  
(  
select * from Employees  
where ExitDate is not null  
) as R2;  
```  
  
---  
# More Queries  
## Exists Operator  
  
```sql  
  
-- it returns true/false based on a select statement  
-- records = 0 => false  
-- records >= 1 => true  
  
select result = 'yes'  
where exists (select * from Customers);  
  
-- imagine this as two nested for loops  
select * from Customers T1  
where exists   
(   
	select * from Orders  
	where customerID= T1.CustomerID and Amount < 1000  
)  
  
-- More optimized and faster  
select * from Customers T1  
where exists   
(   
	select top 1 * from Orders  
	where customerID= T1.CustomerID and Amount < 600  
)  
  
-- More optimized and faster  
select * from Customers T1  
where exists   
(   
	select top 1 R='Y'  from Orders  
	where customerID= T1.CustomerID and Amount < 600  
)  
```  
  
## Union  
  
```sql  
-- the columns of the result-sets must be  
	-- in the same order  
	-- same number of columns  
	-- columns must have same datatypes  
select * from ActiveEmployees  
union  
select * from ResignedEmployees;  
  
-- by default "union" removes duplications  
select * from Countries  
union  
select * from Countries;  
-- you can get all records in this way  
select * from Countries  
union all  
select * from Countries;  
```  
  
> The column names in the result-set are usually equal to the column names in the first `SELECT` statement.  
  
## Case  
  
```sql  
-- like if-elseif-else  
-- if the value of the column Gendor is "f" then put "female" in the new column, GenderType, etc  
select ID, FirstName, LastName, GenderType =   
case  
	when Gendor='m' then 'Male'  
	when Gendor='f' then 'Female'  
	else 'Unknown'  
end  
from Employees;  
  
-- you can put more than one "case"  
-- for example, you can create a view for this!  
select ID, FirstName, LastName, GenderType =   
case  
	when Gendor='m' then 'Male'  
	when Gendor='f' then 'Female'  
	else 'Unknown'  
end, Status =   
case  
	when ExitDate is null then 'Active'  
	when ExitDate is not null then 'Resigned'  
end  
from Employees;  
  
-- you can make calculations/expressions  
select ID, FirstName, LastName, MonthlySalary , NewSalary =   
case  
	when Gendor='m' then MonthlySalary * 1.1  
	when Gendor='f' then MonthlySalary * 1.2  
end  
from Employees;  
  
-- this is like a shorhand  
select ID, FirstName, LastName, GenderType =   
case Gendor  
	when 'm' then 'Male'  
	when 'f' then 'Female'  
	else 'Unknown'  
end  
from Employees;  
  
-- if no condition is true, and there isn't an ELSE part, it returns NULL  
```  
  
---  
# Constraints  
  
```sql  
-- we specify the constraints when creating a table or altering it  
-- constraints help you make sure that your data is valid all the time  
  
-- ensures that a column can't have a null value  
NOT NULL  
  
-- ensures that all values in a column are different  
UNIQUE  
  
-- NOT NULL and UNIQUE  
PRIMARY KEY  
  
-- prevents actions that would destroy links between tables  
FOREIGN KEY  
  
-- ensures that the values in a column satisfies a specific condition  
CHECK  
  
-- sets a default value for a column if no value is specified  
DEFAULT  
  
-- used to create and retrieve data from the database very quickly  
CREATE INDEX  
```  
  
## Primary Key Constraint  
  
```sql  
-- syntax  
CREATE TABLE Persons (    
   ID int NOT NULL PRIMARY KEY,    
   LastName varchar(255) NOT NULL,    
   FirstName varchar(255),    
   Age int    
);  
  
-- to name the primary key, or put multiple fields as a primary key  
CREATE TABLE Persons (    
   ID int NOT NULL,    
   LastName varchar(255) NOT NULL,    
   FirstName varchar(255),    
   Age int,    
   CONSTRAINT PK_Person PRIMARY KEY (ID,LastName)    
);  
  
-- for sure, to add a PK constraint to an existing table, the values must be not null and unique  
ALTER TABLE Persons    
ADD PRIMARY KEY (ID);  
  
ALTER TABLE Persons    
ADD CONSTRAINT PK_Person PRIMARY KEY (ID,LastName);  
  
-- to drop  
ALTER TABLE Persons    
DROP CONSTRAINT PK_Person;  
```  
  
## Foreign Key Constraint  
```sql  
-- a PK in another table  
CREATE TABLE Orders (    
   OrderID int NOT NULL PRIMARY KEY,    
   OrderNumber int NOT NULL,    
   PersonID int FOREIGN KEY REFERENCES Persons(PersonID)    
);    
  
-- to name it, or make it consists of multiple fields  
CREATE TABLE Orders (    
   OrderID int NOT NULL,    
   OrderNumber int NOT NULL,    
   PersonID int,    
   PRIMARY KEY (OrderID),    
   CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)    
);  
  
ALTER TABLE Orders    
ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);  
  
ALTER TABLE Orders    
ADD CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);  
  
-- to drop  
ALTER TABLE Orders    
DROP CONSTRAINT FK_PersonOrder;  
```  
  
## Not Null Constraint  
  
```sql  
CREATE TABLE Persons (    
   ID int NOT NULL,    
    LastName varchar(255) NOT NULL,    
   FirstName varchar(255) NOT NULL,    
   Age int    
);  
  
ALTER TABLE Persons    
ALTER COLUMN Age int NOT NULL;  
```  
  
## Default Constraint  
  
```sql  
CREATE TABLE Persons (    
   ID int NOT NULL,    
   LastName varchar(255) NOT NULL,    
   FirstName varchar(255),    
   Age int,    
   City varchar(255) DEFAULT 'Amman'    
);  
  
-- you can use functions  
CREATE TABLE Orders (    
   ID int NOT NULL,    
   OrderNumber int NOT NULL,    
   OrderDate date DEFAULT GETDATE()    
);  
  
ALTER TABLE Persons    
ADD CONSTRAINT df_City    
DEFAULT 'Amman' FOR City;  
  
ALTER TABLE Persons    
DROP Constraint  df_City;  
```  
  
```sql  
create table test (  
	id int not null,  
	name1 nvarchar(100) not null default 'name1',  
	name2 nvarchar(100) null default 'name2'  
)  
  
-- you can insert like this  
insert into test values (1, default, default);  
-- 1 name1 name2  
insert into test (id) values (2);  
-- 2 name1 name2  
  
-- in this case, for name2  
	-- if the default constraint is set, the engine will insert the constraint value whether the field is nullable or not  
	-- if the default constraint is not set, the engine will insert null if the field allows nulls, and show an error otherwise  
insert into test (id, name1) values  
(12, 'name');  
```  
  
## Check Constraint  
  
```sql  
CREATE TABLE Persons (    
   ID int NOT NULL,    
   LastName varchar(255) NOT NULL,    
   FirstName varchar(255),    
   Age int CHECK (Age>=18)    
);  
  
-- to allow naming and for defining the constraint on multiple columns  
CREATE TABLE Persons (    
   ID int NOT NULL,    
   LastName varchar(255) NOT NULL,    
   FirstName varchar(255),    
   Age int,    
   City varchar(255),    
   CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Amman')    
);  
  
-- to drop  
ALTER TABLE Persons    
DROP CONSTRAINT CHK_Person;  
```  
  
## Unique Constraint  
  
```sql  
-- you can have many unique constraint per table  
-- you can have one PK constraint per table  
CREATE TABLE Persons (    
   ID int NOT NULL UNIQUE,    
   LastName varchar(255) NOT NULL,    
   FirstName varchar(255),    
   Age int    
);  
  
-- to allow naming and for defining the constraint on multiple columns  
CREATE TABLE Persons (    
   ID int NOT NULL,    
   LastName varchar(255) NOT NULL,    
   FirstName varchar(255),    
   Age int,    
   CONSTRAINT UC_Person UNIQUE (ID,LastName)    
);  
  
ALTER TABLE Persons    
ADD UNIQUE (ID);  
  
ALTER TABLE Persons    
ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);  
  
ALTER TABLE Persons    
DROP CONSTRAINT UC_Person;  
  
-- note that you can have only one NULL in your table, because two NULLs are considered as duplicated values  
```  
  
## SQL Index  
  
```sql  
-- if we have indexes, updating/inserting data takes more time, because, indexes need to be updated/inserted too.  
CREATE INDEX idx_lastname    
ON Persons (LastName);  
  
-- on many columns  
CREATE INDEX idx_pname    
ON Persons (LastName, FirstName);  
  
-- duplicated values are not allowed  
CREATE UNIQUE INDEX _index_name_    
ON _table_name_ (_column1_, _column2_, ...);  
  
DROP INDEX table_name.index_name;  
  
-- when you create a table with PK, Sql server automatically creates a clustered index that includes the PK columns.  
-- clustered index is faster than the normal index.  
-- create indices on the columns you query a lot.  
  
-- the cluster index should be on the PK, because:  
	-- the PK is the most used column  
	-- the cluster index is the fastest index  
	-- we can create one cluster index per table  
```  
  
---  
# Normalization  
## 1NF  
- PK for each table.  
- Atomic/indivisible values.  
- Distinct name for each column. Don't repeat groups of columns. (I don't know what the second sentence mean).  
## 2NF  
- A table must first be in 1NF.  
- No partial dependencies: Each non-key column in the table must be fully dependent on the entire primary key.  
  
## 3NF  
- Table must first be in 1NF and 2NF.  
- No transitive dependencies: Each non-key column in the table must be dependent only on the primary key, and not on any other non-key column.  
---  
Keep practicing - always practice.  
  
---  
# Questions  
Why is a database often much faster at searching/manipulating a large amount of data than code I write myself?  
DBMSs are specialized pieces of software built specifically for data.  
