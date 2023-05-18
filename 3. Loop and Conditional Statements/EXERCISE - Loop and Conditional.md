# Example of Printing Number using Loop

## Using Loop
```
declare
a number:=1;
b number:=10;
begin
LOOP
    DBMS_OUTPUT.PUT_LINE('Current number : ' || a);
    a:=a+1;
    EXIT WHEN a>=b;
END LOOP;
end;
```

## Using While Loop
```
declare
a number:=1;
b number:=10;
begin
WHILE a<=b LOOP
    DBMS_OUTPUT.PUT_LINE('Current number : ' || a);
    a:=a+1;
END LOOP;
end;
```

## Using For Loop
```
declare
a number:=1;
b number:=10;
begin
FOR c IN a..b LOOP
    DBMS_OUTPUT.PUT_LINE('Current number : ' || c);
END LOOP;
end;
```

# Usage of GOTO Statement

## Usage GOTO 
Using GOTO To skip to End Statement when no number Doesn't Satisfy the Assigned Value.
```
declare
a number:=1;
b number:=1;
c number;
d number;
begin
c:=5;
if c=1 then
    d:=a-b;
elsif c=2 then
    d:=a+b;
elsif c=3 then
    d:=a*b;
elsif c=4 then
    d:=a/b;
else
    DBMS_OUTPUT.PUT_LINE('Not valid Choice');
    GOTO SKIP;
end if;
DBMS_OUTPUT.PUT_LINE('c is equal : ' || c);
<<SKIP>>
NULL;
end;
```

# Assignment
![alt text](https://raw.githubusercontent.com/muhk01/plsql_exercise/main/3.%20Loop%20and%20Conditional%20Statements/8c1af799-e659-4dce-96f5-96f0482dceb6.png)
## Create and Insert value to Table.
```
create table cust_charge(cno number(3) primary key, meter_no number(3) unique, prev_reading number(3), current_reading number(3), units number(5), bill_amount number(38));
insert into cust_charge values (89,100,300,800,0,0);
insert into cust_charge values (67,101,200,800,0,0);
insert into cust_charge values (90,200,100,800,0,0);
```
## Calculate Units and Bills Total
```
declare
v_cols cust_charge%rowtype;
v_bills number:=0;
v_extras number:=0;
v_bills_total number:=0;
u number;
begin
select * into v_cols from cust_charge where cno = 89;
    u:=v_cols.current_reading - v_cols.prev_reading;
    for c in 1..u loop
        if(c < 100) then
            v_bills:=v_bills + 0.5;
        else
            v_extras:=v_extras + 0.75;
        end if;
    end loop;
    v_bills_total:= v_bills + v_extras;
    update cust_charge set units = u, bill_amount = v_bills_total
    where cno=89;
    DBMS_OUTPUT.PUT_LINE(v_bills_total || ' ' || u);
end;
```
