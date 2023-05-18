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

But since in OTHERS any error occurs will trapped into OTHERS exception, we must specify Error CODE, like below :
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

