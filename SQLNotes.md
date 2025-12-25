DATA - Any kind of information

DataBase - It is a software which is used to store the data/information either permanently or temporily. 
               Mysql(Python)
               MSSQL(.Net)

------------------------------------------------------------------------------
SQL(Structured Query Language) 

- It is query language which is used to operate,manage and access database.

-By using different query we can create, delete, retrieve, add or access the information/data in database.

-One of the great advantage of sql is that it can use a single command to access multiple records within a database.

------------------------------------------------------------------------------
RDBMS(Relational Database Management system)

- Relational Database basically defines database in the form of table.

-RDBMS is basically a s/w which is used to maintain a relational database.

- it uses sql to perform the operation on data.

->basically, it contains row and col

------------------------------------------------------------------
Normalisation

- It is the process to remove the duplication in the database and improve integrity and update the data without causing error or inconsistencies

Types
-----
1.1NF(First Normal Form) - to remove multiple values in once cell.
2.2NF (Second Normal Form) - removes the dependencies on the column.
3.3NF(Third Normal Form) - removes indirect dependency
4.BCNF(Boyce-Codd Normal Form) - to determine the primary column and create new dependency.
------------------------------------------------------------------------------

Classification of sql


                                 SQL
                                  |
          ------------------------------------------------
          |                       |                      |                   
         DDL                     DML                    DQL
          |                       |                      |
        -CREATE               -INSERT                 -SELECT
        -DROP                 -UPDATE
        -ALTER                -DELETE
        -TRUNCATE             

DDL(Data Definition Language)

- It is a set of commands to create,modify and delete database structure but not the data.

->CREATE TABLE: it creates a new table in database.

->DROP TABLE: it is used to delete both the structure and all the data stored in the table.

->ALTER TABLE: it is used to add, delete, or modify columns in the existing table(structure).

->TRUNCATE TABLE: it is used to delete the data inside the table and free the space.

==============================================================================

DML(Data Manipulation Language)

-It is used to modify the database.

->INSERT: It is used to insert data into the row of a table.

->UPDATE: It is used to update or modify the value of a column in the table.

->DELETE: It is used to remove one or more row from a table.

==============================================================================

DQL(Data Query Language)

- It is used to fetch the data from the database.

->SELECT: It is used to retrieve data from the database.

------------------------------------------------------------------------------
SQL DATATYPE

String datatype-

-varchar(n)/varchar2(n) where n is predefined size by the user.
-char(n)

Number datatype-

-number(p,s) where p = total number of digits , s=two digits after decimal

Time and Date datatype-

-Date 
-timestamp - yyyy:mm:dd and hh:mm:ss

-----------------------------------------------------------------------------------------
SQL Constraint

The following constraints are commonly used in SQL:

->NOT NULL - Ensures that a column cannot have a NULL value

->UNIQUE - Ensures that all values in a column are different

->PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in 
                a table

->FOREIGN KEY - Uniquely identifies a row/record in another table

->CHECK - Ensures that all values in a column satisfies a specific condition
          ex - Check (age>=18)

->DEFAULT - Sets a default value for a column when no value is specified.

------------------------------------------------------------------------------------------
--create

create table Employee(
eid number(10) NOT NULL PRIMARY KEY,
ename varchar(25) NOT NULL,
age number(3),
salary number(8,2),
gender char(1) 
);



--alter
alter table Employee add Phone_number number(10);

alter table Employee add designation varchar(8);

alter table Employee
  rename column Phone_number TO mobileNo;

alter table Employee drop column mobileNo;



--insert

insert into Employee (eid,ename,age,salary,gender,designation)values(101, 'alex', 20 ,450000.00, 'M', 'AST');

insert into Employee VALUES (102, 'peter', 18 , 147220.00, 'M','AST');
insert into Employee VALUES (103, 'sabrina', 24 , 947380.00,  'F','ITA');
insert into Employee VALUES (104, 'akansha', 21, 256000.00,  'F','ASE');
insert into Employee VALUES (109, 'farshiya', 21, 974000.00,  'F','AST');

insert into Employee(eid,ename) VALUES(105,'sona');
insert into Employee(eid,ename) VALUES(106,'aakash');


--select

select * from Employee;

Select eid,ename,salary from Employee;



--Update

update Employee set age=21, salary= 700000.00, designation= 'ASE' where eid=106;

update Employee set gender='F',age=25 where eid = 105;



--delete

delete from Employee where eid=102;


===========================================================================
Aggregate function

->MIN() function- returns the smallest value of the selected column.
->MAX() function- returns the largest value of the selected column.
->COUNT() function- returns the number of rows that matches a specified criteria.
->AVG() function- returns the average value of a numeric column.
->SUM() function- returns the total sum of a numeric column.

select max(salary) from Employee;
select max(salary) as Highest_Salary from Employee;

select avg(salary) from Employee;
select min(salary) from Employee;
select sum(salary) from Employee;

select count(*) from Employee;
select count(designation) from Employee;

==============================================================================

-->distinct- to eliminate all duplicate records and fetch only unique records.

select distinct(designation) from Employee;



-->Like Operator

- it is used in a WHERE clause to search for a specified pattern in a column.

-> % - The percent sign represents zero, one, or multiple characters
-> _ - The underscore represents a single character

(Can also be used in combination)


--To fetch data which start with "a"

 select * from Employee where ename LIKE 'a%';


--To fetch data which end with "a"

 select * from Employee where ename LIKE '%a';


--To fetch data which contain "i" in between

 select * from Employee where ename LIKE '%i%';


--To fetch data which has "a" as second character

 select * from Employee where ename LIKE '_a%';


--To fetch data which start with "s" and has atleast 3 characters

 select * from Employee where ename LIKE 's__%';


--To fetch data which starts with "a" and ends with "x"

 select * from Employee where ename like 'a__x';

===================================================================
--Null/not Null

select * from Employee where designation is null;

select * from Employee where designation is not null;

--In/not in

select * from Employee where designation in('ASE','ITA');
select * from Employee where designation not in('ASE','ITA');

-- AND/OR

select * from Employee where ename like 'a%' and age=21;
select * from Employee where ename like 'a%' or age =21;

--BETWEEN

SELECT * FROM Employee WHERE age BETWEEN 18 AND 24;

===============================================================================
Sorting in SQL

Order by- used for sorting the data in ascending and descending order based on one or more
          columns.

select * from Employee order by age;
select * from Employee order by age desc;

===============================================================================

--truncate

truncate table Employee;

--drop

drop table Employee;

===============================================================================
Operator used in where clause

> greater than

< less than

>= greater than equal to

<= less than equal to

<> not equal to

= eqaul to

select * from Employee where salary <> 450000.00;

==================================================================================
Clauses in SQL

--Group by- Groups rows that share a property so that the aggregate function can be applied 
            to each group.

select count(*),designation from Employee group by designation;


--Having- It selects among the groups defined by the GROUP BY clause.It is basically a filter same 
          as where clause. Where clause cannot be used with aggregate function so Having is used 
          in place of where to filter the data.

select count(*),designation from Employee 
group by designation 
having count(*)>1;

------------------------------------------------------------------

select count(*),designation from Employee
group by designation 
having count(*)>1;
order by designation DESC


==============================================================================
Subquery

-Subquery has an inner query and outer query. Inner query is executed first and the result is then 
 again executed with outer query.

--to find max salary

 select * from Employee where salary = (select max(salary) from Employee);


--to find min salary

 select * from Employee where salary = (select min(salary) from Employee);
 
--to find second max salary

 select max(salary) from Employee where salary < (select max(salary) from Employee);

--to find second min salary
 
 select min(salary) from Employee where salary < (select min(salary) from Employee);

 ==============================================================================
Foreign key concept

- a foreign key is a field or a column that is used to establish a link between two table

TABLE NAME:DEPT - PARENT TABLE
did primary key
dept_name not null

TABLE NAME:EMPLOYEE - CHILD TABLE
eid primary key
ename not null
age check(age>=21)
dept_id references Dept(did) - foreign key





create table Dept(
deptid number(10) primary key,
dname varchar(15) not null
);

insert into Dept values(1,'IT');
insert into Dept values(2,'ITIS');
insert into Dept values(3,'EIS');
insert into Dept values(4,'CBO');

insert into Dept values(1,'Innovation');

create table Emp(
eid number(10) primary key,
ename varchar(25),
age number(3) check(age>=21),
location varchar(15) default 'Mumbai',
depid number(10) references Dept(deptid)
);

insert into Emp values(101,'Rithika',22,'chennai',1);
insert into Emp values(102,'Pranav',21,'chennai',2);
insert into Emp values(103,'sara',21,'Pune',2);
insert into Emp values(105,'sagar',25,'Delhi',3);

insert into Emp values(107,'supriya',18,'Delhi',10);

insert into Emp(eid,ename) values(78,'Preeti');
insert into Emp(eid,ename) values(40,'Roshni');


=====================================================================
Joins in sql

-to combine two or more tables

-The joining of two or more tables is based on common field between them.

->inner join - Returns records that have matching values in both tables

->left join- Returns all records from the left table, and the
             matched records from the right table

->right join-  Returns all records from the right table, and the
               matched records from the left table

->full join - Returns all records when there is a match in either
             left or right table



--inner join

select * from Dept inner join Emp on Dept.deptid=Emp.depid;


--left join

select * from Dept left join Emp on Dept.deptid=Emp.depid;


--right join

select * from Dept right join Emp on Dept.deptid=Emp.depid;


--full join

select * from Dept full join Emp on Dept.deptid=Emp.depid;
