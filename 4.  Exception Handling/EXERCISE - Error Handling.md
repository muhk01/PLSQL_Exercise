# Handling Error Using OTHERS

When not sure what Error Code will occurs we could using OTHER to catch the error, example :
Supposed we having table _emp_exc_ with following columns.
```
create table emp_exc(empno number(4), name char(30), job char(20), sal number(8));
```

Insert to the table
```
insert into emp_exc(empno, name, job, sal) values (1,'Raj','prof',96000);
insert into emp_exc(empno, name, job, sal) values (2,'Amar','assoc prof',80000);
```

And we want to SELECT which empno is never exists in table, oracle will raise error  "ORA-01403: no data found.", therefore, we could handle with
```
declare
v_name emp_exc.name%type;
begin
select name into v_name 
from emp_exc where empno=21;
DBMS_OUTPUT.PUT_LINE('Name ' || v_name);
exception
WHEN OTHERS THEN
DBMS_OUTPUT.PUT_LINE('Some error occurs please check');
end;
```

But since in OTHERS any error occurs will trapped into OTHERS exception, we must specify Error , like below :
```
declare
v_name emp_exc.name%type;
begin
select name into v_name 
from emp_exc where empno=21;
DBMS_OUTPUT.PUT_LINE('Name ' || v_name);
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    -- Handle the exception appropriately.
    DBMS_OUTPUT.PUT_LINE('No data found.');
END;
```
Another Example to handle such ZERO_DIVIDED :
```
declare
v_a number:=1;
v_b number:=0;
v_c number;
begin
v_c:=v_a/v_b;
exception
WHEN ZERO_DIVIDE THEN
DBMS_OUTPUT.PUT_LINE('Divided By Zero');
end;
```

In Oracle Every error CODE has Error Number, we also able to catch using Error Number Instead of Code, here to handle error Code "ORA-01476 for ZERO_DIVIDE"
```
declare
v_a number:=1;
v_b number:=0;
v_c number;
DIVISION_ZERO EXCEPTION;
PRAGMA EXCEPTION_INIT(DIVISION_ZERO,-01476);
begin
v_c:=v_a/v_b;
EXCEPTION
WHEN DIVISION_ZERO THEN
DBMS_OUTPUT.PUT_LINE('Divided By Zero');
end;
```

# Custom Exception.
Write Pre defined exception PLSQL To check whether items it in stock or out stock in _Item_ Table.
Supposed we has table with following columns.
```
--create table
create table item(item_no number(3) primary key, name char(30), rate number(3), qty_in_stock number(5));
create table item_order(order_no number(3) primary key, item_no number(3), name char(30), qty number(3));
```
Inserting into Item Table
```
insert into item values(1,'pen',10,1000);
insert into item values(2,'pencil',10,4);
```
Exception Handling 
--Pre defined Exception
declare 
out_of_stock EXCEPTION;
v_rec item%rowtype;
begin
select * into v_rec from item where item_no=2;
if v_rec.qty_in_stock < 5 then
    raise out_of_stock;
end if;
dbms_output.put_line('qty_in_stock ' || v_rec.qty_in_stock);
exception
when out_of_stock then
dbms_output.put_line('Item out of Stock');
end;
```
