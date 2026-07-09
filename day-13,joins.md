Joins

=====

a join in MySQL is used to combine rows from 2 or more tables based on related columns

e.g.:

\---

employees table-->employee details

department table-->department details

if you want to see which employee belongings to which department you need to join these 2 tables.



why do we need joins?

1.To fetch data from multiple tables in a single query

2.to reduce data duplication instead of keeping everything in one table.

3.to implement relationships like(one-to-one,one-to-many,many-to-one,many-to-many)

4.to generate reports and analytics combinng different data sets.



Types of joins

\------------

1.inner join

2.left join

3.right join

4.full join

5.cross join

6.self join



1.inner join

\-------------

returns only rows that have matching values in both tables

syntax

\----------

select columns

from table1

inner join table2

on table1.common\_column=table2.common\_column;



2.left join

\-----------

retunes all rows from the left table and the matched rows from the right table. if no match null values appear for right table columns

syntax

\--------

select columns

from table1

left join table2

on table1.common\_column=table2.common\_column;



3.right join

\-----------

retunes all rows from the right table and the matched rows from the left table. if no match null values appear for left table column

syntax

\-----------

select columns

from table1

right join table2

on table1.common\_column=table2.common\_column;

4.full join

\-----------

to simulate use union of left join and right join

syntax

\---------

select columns

from table1

left join table2

on table1.common\_column=table2.common\_column

union

select columns

from table1

right join table2

on table1.common\_column=table2.common\_column;



5.cross join or Cartesian product

\-------------

retunes cartesian product every row from the first table with every row from the second table

syntax

\-------

select columns

from table1

cross join table2;

6.self join

\-----------

a table joined with itself.

syntax

\------

select a.columns,b.columns

from table1 as a

inner join table1 as b

on a.common\_column=b.common\_column;





mysql> use da3;

Database changed

mysql> create table tab1(numid int(3));

Query OK, 0 rows affected, 1 warning (0.36 sec)



mysql> create table tab2(numid int(3));

Query OK, 0 rows affected, 1 warning (0.33 sec)



mysql> insert into tab1 values(10),(11),(12),(14);

Query OK, 4 rows affected (0.03 sec)

Records: 4  Duplicates: 0  Warnings: 0



mysql> insert into tab2 values(11),(12),(13),(14);

Query OK, 4 rows affected (1.11 sec)

Records: 4  Duplicates: 0  Warnings: 0



mysql> select\*from tab1;

+-------+

| numid |

+-------+

|    10 |

|    11 |

|    12 |

|    14 |

+-------+

4 rows in set (0.00 sec)



mysql> select\*from tab2;

+-------+

| numid |

+-------+

|    11 |

|    12 |

|    13 |

|    14 |

+-------+

4 rows in set (0.00 sec)



mysql> select\*from tab1

&#x20;   -> inner join tab2

&#x20;   -> on

&#x20;   -> tab1.numid=tab2.numid;

+-------+-------+

| numid | numid |

+-------+-------+

|    11 |    11 |

|    12 |    12 |

|    14 |    14 |

+-------+-------+

3 rows in set (2.01 sec)



mysql> -- left join==>matched records +left table records

mysql> select\*from tab1

&#x20;   -> left join tab2

&#x20;   -> on

&#x20;   -> tab1.numid=tab2.numid;

+-------+-------+

| numid | numid |

+-------+-------+

|    10 |  NULL |

|    11 |    11 |

|    12 |    12 |

|    14 |    14 |

+-------+-------+

4 rows in set (0.14 sec)



mysql> -- rightjoin-->matched records\_right table records

mysql> select\*from tab1

&#x20;   -> right join tab2

&#x20;   -> on

&#x20;   -> tab1.numid=tab2.numid;

+-------+-------+

| numid | numid |

+-------+-------+

|    11 |    11 |

|    12 |    12 |

|  NULL |    13 |

|    14 |    14 |

+-------+-------+

4 rows in set (1.62 sec)



Note: Full join

0

mysql> select\*from tab1

&#x20;   -> left join tab2

&#x20;   -> on

&#x20;   -> tab1.numid=tab2.numid

&#x20;   -> union

&#x20;   -> select\*from tab1

&#x20;   -> right join tab2

&#x20;   -> on

&#x20;   -> tab1.numid=tab2.numid;

+-------+-------+

| numid | numid |

+-------+-------+

|    10 |  NULL |

|    11 |    11 |

|    12 |    12 |

|    14 |    14 |

|  NULL |    13 |

+-------+-------+

5 rows in set (1.69 sec)



mysql> select\*from tab1

&#x20;   -> cross join tab2;

+-------+-------+

| numid | numid |

+-------+-------+

|    14 |    11 |

|    12 |    11 |

|    11 |    11 |

|    10 |    11 |

|    14 |    12 |

|    12 |    12 |

|    11 |    12 |

|    10 |    12 |

|    14 |    13 |

|    12 |    13 |

|    11 |    13 |

|    10 |    13 |

|    14 |    14 |

|    12 |    14 |

|    11 |    14 |

|    10 |    14 |

+-------+-------+

16 rows in set (0.00 sec)



mysql> show tables;

+------------------+

| Tables\_in\_da3    |

+------------------+

| course           |

| course\_completed |

| department       |

| emp              |

| employee         |

| employees        |

| employes         |

| orders           |

| products         |

| sales            |

| students         |

| studentscores    |

| tab1             |

| tab2             |

+------------------+

14 rows in set (0.07 sec)



mysql> drop database da3;

Query OK, 14 rows affected (7.63 sec)



mysql> show databases;

+--------------------+

| Database           |

+--------------------+

| information\_schema |

| mysql              |

| performance\_schema |

| sys                |

+--------------------+

4 rows in set (0.00 sec)



mysql> use mysql;

Database changed

mysql> CREATE TABLE Employees (

&#x20;   ->     emp\_id INT PRIMARY KEY,

&#x20;   ->     name VARCHAR(100),

&#x20;   ->     department\_id INT,

&#x20;   ->     salary DECIMAL(10,2)

&#x20;   -> );

Query OK, 0 rows affected (0.07 sec)



mysql>

mysql> INSERT INTO Employees (emp\_id, name, department\_id, salary) VALUES

&#x20;   -> (101, 'Arjun', 1, 50000),

&#x20;   -> (102, 'Bhavana', 2, 65000),

&#x20;   -> (103, 'Charan', 2, 72000),

&#x20;   -> (104, 'Divya', 3, 45000),

&#x20;   -> (105, 'Eswar', NULL, 40000),

&#x20;   -> (106, 'Farhan', 4, 55000),

&#x20;   -> (107, 'Gowri', 2, 62000),

&#x20;   -> (108, 'Harish', 5, 48000),

&#x20;   -> (109, 'Ishita', NULL, 53000),

&#x20;   -> (110, 'Jagan', 3, 60000);

Query OK, 10 rows affected (0.49 sec)

Records: 10  Duplicates: 0  Warnings: 0



mysql> CREATE TABLE Departments (

&#x20;   ->     department\_id INT PRIMARY KEY,

&#x20;   ->     department\_name VARCHAR(100)

&#x20;   -> );

Query OK, 0 rows affected (0.40 sec)



mysql>

mysql>

mysql> INSERT INTO Departments (department\_id, department\_name) VALUES

&#x20;   -> (1, 'Human Resources'),

&#x20;   -> (2, 'Engineering'),

&#x20;   -> (3, 'Marketing'),

&#x20;   -> (4, 'Finance'),

&#x20;   -> (5, 'Operations');

Query OK, 5 rows affected (2.30 sec)

Records: 5  Duplicates: 0  Warnings: 0



mysql>

mysql> CREATE TABLE Projects (

&#x20;   ->     project\_id INT PRIMARY KEY,

&#x20;   ->     project\_name VARCHAR(100),

&#x20;   ->     emp\_id INT

&#x20;   -> );

Query OK, 0 rows affected (0.14 sec)



mysql>

mysql> INSERT INTO Projects (project\_id, project\_name, emp\_id) VALUES

&#x20;   -> (201, 'Website Redesign', 102),

&#x20;   -> (202, 'Mobile Banking App', 103),

&#x20;   -> (203, 'Marketing Campaign', 104),

&#x20;   -> (204, 'Payroll System', 106),

&#x20;   -> (205, 'Backend Optimization', 107),

&#x20;   -> (206, 'Cloud Migration', 102),

&#x20;   -> (207, 'Customer Analytics', 110),

&#x20;   -> (208, 'Inventory System', NULL);

Query OK, 8 rows affected (0.04 sec)

Records: 8  Duplicates: 0  Warnings: 0



mysql> select\*from employees;

+--------+---------+---------------+----------+

| emp\_id | name    | department\_id | salary   |

+--------+---------+---------------+----------+

|    101 | Arjun   |             1 | 50000.00 |

|    102 | Bhavana |             2 | 65000.00 |

|    103 | Charan  |             2 | 72000.00 |

|    104 | Divya   |             3 | 45000.00 |

|    105 | Eswar   |          NULL | 40000.00 |

|    106 | Farhan  |             4 | 55000.00 |

|    107 | Gowri   |             2 | 62000.00 |

|    108 | Harish  |             5 | 48000.00 |

|    109 | Ishita  |          NULL | 53000.00 |

|    110 | Jagan   |             3 | 60000.00 |

+--------+---------+---------------+----------+

10 rows in set (0.57 sec)



mysql> select\*from departments;

+---------------+-----------------+

| department\_id | department\_name |

+---------------+-----------------+

|             1 | Human Resources |

|             2 | Engineering     |

|             3 | Marketing       |

|             4 | Finance         |

|             5 | Operations      |

+---------------+-----------------+

5 rows in set (0.00 sec)



mysql> select\*from projects;

+------------+----------------------+--------+

| project\_id | project\_name         | emp\_id |

+------------+----------------------+--------+

|        201 | Website Redesign     |    102 |

|        202 | Mobile Banking App   |    103 |

|        203 | Marketing Campaign   |    104 |

|        204 | Payroll System       |    106 |

|        205 | Backend Optimization |    107 |

|        206 | Cloud Migration      |    102 |

|        207 | Customer Analytics   |    110 |

|        208 | Inventory System     |   NULL |

+------------+----------------------+--------+

8 rows in set (0.00 sec)



mysql> -- get all employees with their department name

mysql> select e.emp\_id,

&#x20;   -> e.name,d.department\_name

&#x20;   -> from employees e

&#x20;   -> inner join departments d

&#x20;   -> on e.department\_id=d.department\_id;

+--------+---------+-----------------+

| emp\_id | name    | department\_name |

+--------+---------+-----------------+

|    101 | Arjun   | Human Resources |

|    102 | Bhavana | Engineering     |

|    103 | Charan  | Engineering     |

|    104 | Divya   | Marketing       |

|    106 | Farhan  | Finance         |

|    107 | Gowri   | Engineering     |

|    108 | Harish  | Operations      |

|    110 | Jagan   | Marketing       |

+--------+---------+-----------------+

8 rows in set (0.00 sec)



\-->list all employees who's are assigned to a project



mysql> select distinct e.emp\_id,e.name

&#x20;   -> from employees e

&#x20;   -> inner join projects p

&#x20;   -> on e.emp\_id=p.emp\_id;

+--------+---------+

| emp\_id | name    |

+--------+---------+

|    102 | Bhavana |

|    103 | Charan  |

|    104 | Divya   |

|    106 | Farhan  |

|    107 | Gowri   |

|    110 | Jagan   |

+--------+---------+

6 rows in set (0.00 sec)

\-->show employees names and their project names

mysql> select e.name,p.project\_name

&#x20;   -> from employees e

&#x20;   -> inner join projects p

&#x20;   -> on e.emp\_id=p.emp\_id;

+---------+----------------------+

| name    | project\_name         |

+---------+----------------------+

| Bhavana | Website Redesign     |

| Charan  | Mobile Banking App   |

| Divya   | Marketing Campaign   |

| Farhan  | Payroll System       |

| Gowri   | Backend Optimization |

| Bhavana | Cloud Migration      |

| Jagan   | Customer Analytics   |

+---------+----------------------+

7 rows in set (0.00 sec)

\--->list all employees and their department names(even if no department assigned)

mysql> select e.emp\_id,e.name,d.department\_name

&#x20;   -> from employees e

&#x20;   -> left join departments d

&#x20;   -> on e.department\_id=d.department\_id;

+--------+---------+-----------------+

| emp\_id | name    | department\_name |

+--------+---------+-----------------+

|    101 | Arjun   | Human Resources |

|    102 | Bhavana | Engineering     |

|    103 | Charan  | Engineering     |

|    104 | Divya   | Marketing       |

|    105 | Eswar   | NULL            |

|    106 | Farhan  | Finance         |

|    107 | Gowri   | Engineering     |

|    108 | Harish  | Operations      |

|    109 | Ishita  | NULL            |

|    110 | Jagan   | Marketing       |

+--------+---------+-----------------+

10 rows in set (0.00 sec)

\--->show all employees and their project names (if assigned)

mysql> select e.name,p.project\_name

&#x20;   -> from employees e

&#x20;   -> left join projects p

&#x20;   -> on e.emp\_id=p.emp\_id;

+---------+----------------------+

| name    | project\_name         |

+---------+----------------------+

| Arjun   | NULL                 |

| Bhavana | Cloud Migration      |

| Bhavana | Website Redesign     |

| Charan  | Mobile Banking App   |

| Divya   | Marketing Campaign   |

| Eswar   | NULL                 |

| Farhan  | Payroll System       |

| Gowri   | Backend Optimization |

| Harish  | NULL                 |

| Ishita  | NULL                 |

| Jagan   | Customer Analytics   |

+---------+----------------------+

11 rows in set (0.00 sec)



\-->get  all departments and the employees working in them.

mysql> select d.department\_name,

&#x20;   -> count(e.emp\_id)as total\_employees

&#x20;   -> from departments d

&#x20;   -> left join employees e

&#x20;   -> on d.department\_id=e.department\_id

&#x20;   -> group by d.department\_name;

+-----------------+-----------------+

| department\_name | total\_employees |

+-----------------+-----------------+

| Human Resources |               1 |

| Engineering     |               3 |

| Marketing       |               2 |

| Finance         |               1 |

| Operations      |               1 |

+-----------------+-----------------+



\-->show al projects and their assigned employees(even if project has no one)

mysql> select p.project\_name,

&#x20;   -> e.name

&#x20;   -> from employees e

&#x20;   -> right join projects p

&#x20;   -> on e.emp\_id=p.emp\_id;

+----------------------+---------+

| project\_name         | name    |

+----------------------+---------+

| Website Redesign     | Bhavana |

| Mobile Banking App   | Charan  |

| Marketing Campaign   | Divya   |

| Payroll System       | Farhan  |

| Backend Optimization | Gowri   |

| Cloud Migration      | Bhavana |

| Customer Analytics   | Jagan   |

| Inventory System     | NULL    |

+----------------------+---------+

8 rows in set (0.00 sec)

\-->list all departments and the employees in them (even if no employee)

mysql> select d.department\_name,e.name

&#x20;   -> from employees e

&#x20;   -> right join departments d

&#x20;   -> on e.department\_id=d.department\_id;

+-----------------+---------+

| department\_name | name    |

+-----------------+---------+

| Human Resources | Arjun   |

| Engineering     | Gowri   |

| Engineering     | Charan  |

| Engineering     | Bhavana |

| Marketing       | Jagan   |

| Marketing       | Divya   |

| Finance         | Farhan  |

| Operations      | Harish  |

+-----------------+---------+

8 rows in set (0.00 sec)

\-->list all employees and the departments they belong to using right join.

mysql> select e.name,

&#x20;   -> d.department\_name

&#x20;   -> from departments d

&#x20;   -> right join employees e

&#x20;   -> on d.department\_id=e.department\_id;

+---------+-----------------+

| name    | department\_name |

+---------+-----------------+

| Arjun   | Human Resources |

| Bhavana | Engineering     |

| Charan  | Engineering     |

| Divya   | Marketing       |

| Eswar   | NULL            |

| Farhan  | Finance         |

| Gowri   | Engineering     |

| Harish  | Operations      |

| Ishita  | NULL            |

| Jagan   | Marketing       |

+---------+-----------------+

10 rows in set (0.00 sec)

\-->get al employees and all departments (even if no match)

mysql> select e.name,d.department\_name

&#x20;   -> from employees  e

&#x20;   -> left join departments d

&#x20;   -> on e.department\_id=d.department\_id

&#x20;   -> union

&#x20;   -> select e.name,d.department\_name

&#x20;   -> from employees e

&#x20;   -> right join departments d

&#x20;   -> on e.department\_id=d.department\_id;

+---------+-----------------+

| name    | department\_name |

+---------+-----------------+

| Arjun   | Human Resources |

| Bhavana | Engineering     |

| Charan  | Engineering     |

| Divya   | Marketing       |

| Eswar   | NULL            |

| Farhan  | Finance         |

| Gowri   | Engineering     |

| Harish  | Operations      |

| Ishita  | NULL            |

| Jagan   | Marketing       |

+---------+-----------------+

10 rows in set (0.00 sec)



mysql>



1.what are the difference between count(\*)from table and count(column)from table?

count(\*) : it counts all records including with null values.

count(column):it does not count the records without null values.



\--->list all projects and employees (even if some don't match)

mysql> select e.name,p.project\_name

&#x20;   -> from employees e

&#x20;   -> left join projects p

&#x20;   -> on e.emp\_id=p.emp\_id

&#x20;   -> union

&#x20;   -> select e.name,p.project\_name

&#x20;   -> from employees e

&#x20;   -> right join projects p

&#x20;   -> on e.emp\_id=p.emp\_id;

+---------+----------------------+

| name    | project\_name         |

+---------+----------------------+

| Arjun   | NULL                 |

| Bhavana | Cloud Migration      |

| Bhavana | Website Redesign     |

| Charan  | Mobile Banking App   |

| Divya   | Marketing Campaign   |

| Eswar   | NULL                 |

| Farhan  | Payroll System       |

| Gowri   | Backend Optimization |

| Harish  | NULL                 |

| Ishita  | NULL                 |

| Jagan   | Customer Analytics   |

| NULL    | Inventory System     |

+---------+----------------------+

12 rows in set (0.00 sec)



mysql> select e.name,count(p.project\_id)as total\_projects

&#x20;   -> from employees e

&#x20;   -> left join projects p

&#x20;   -> on e.emp\_Id=p.emp\_id

&#x20;   -> group by e.name;

+---------+----------------+

| name    | total\_projects |

+---------+----------------+

| Arjun   |              0 |

| Bhavana |              2 |

| Charan  |              1 |

| Divya   |              1 |

| Eswar   |              0 |

| Farhan  |              1 |

| Gowri   |              1 |

| Harish  |              0 |

| Ishita  |              0 |

| Jagan   |              1 |

+---------+----------------+

10 rows in set (0.00 sec)



\-->list all projects and employees (even if someone don't match)

\-->

