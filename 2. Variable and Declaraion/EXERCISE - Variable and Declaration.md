# Assigning Value from SELECT Statement

## Create sample table

Create sample table to hold some values.
```
create table emp_exc(empno number(4), name char(30), job char(20), sal number(8));
```
## Insert Some Value

Insert some value for demonstration purpose for selecting in PL/SQL Block
```
insert into emp_exc(empno, name, job, sal) values (1,'Raj','prof',96000);
insert into emp_exc(empno, name, job, sal) values (2,'Amar','assoc prof',80000);
insert into emp_exc(empno, name, job, sal) values (3,'Rahat','prof',80000);
insert into emp_exc(empno, name, job, sal) values (4,'Rishan','assoc prof',75000);
insert into emp_exc(empno, name, job, sal) values (5,'Ram','prof',95000);
insert into emp_exc(empno, name, job, sal) values (6,'Sukh','assoc prof',60000);
insert into emp_exc(empno, name, job, sal) values (7,'Prem','prof',55000);
```

## PL/SQL Blocks to query selecting column name and job and assign to v_name, and v_job

declaration is defined manually with its type data, make sure when defining variable and assigning value from _SELECT_ has the exact same value for example :
_v_name_ which hold value for column _name_ char has exactly same type, otherwise will return error.

```
declare
v_name char(30);
v_job char(20);
begin
select name,job into v_name,v_job from emp_exc where empno=2;
DBMS_OUTPUT.PUT_LINE('Welcome to PL/SQL');
DBMS_OUTPUT.PUT_LINE('Name ' || v_name);
DBMS_OUTPUT.PUT_LINE('Job ' || v_job);
end;
```

## Usage of %ROWTYPE

Similar as above for declaration but type data replaced correspond to the defined columns using %TYPE, it is the right way incase we dont know the type data each columns.

```
declare
v_name emp_exc.name%type;
v_job emp_exc.job%type;
v_sal emp_exc.sal%type;
v_empno emp_exc.empno%type;
begin
select empno,name,job,sal into v_empno,v_name,v_job,v_sal 
from emp_exc where empno=2;
DBMS_OUTPUT.PUT_LINE('Welcome to PL/SQL');
DBMS_OUTPUT.PUT_LINE('Name ' || v_name);
DBMS_OUTPUT.PUT_LINE('Job ' || v_job);
DBMS_OUTPUT.PUT_LINE('sal  ' || v_sal);
DBMS_OUTPUT.PUT_LINE('emp no ' || v_empno);
end;
```

## Usage of %TYPE

In this case all columns will be declared once inside _v_rec_ which for all type already referred to the table columns. to fetch for each column is using _v_rec.<column_name>_
```
declare
v_rec emp_exc%rowtype;
begin
select * into v_rec 
from emp_exc where empno=2;
DBMS_OUTPUT.PUT_LINE('Welcome to PL/SQL');
DBMS_OUTPUT.PUT_LINE('Name ' || v_rec.name);
DBMS_OUTPUT.PUT_LINE('Job ' || v_rec.job);
DBMS_OUTPUT.PUT_LINE('sal  ' || v_rec.sal);
DBMS_OUTPUT.PUT_LINE('emp no ' || v_rec.empno);
end;
```
