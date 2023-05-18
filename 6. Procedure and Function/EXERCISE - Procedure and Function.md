# Exercise to Comparing USAGE OF PARAMETERS IN OUT, IN, AND OUT
There are three argument modes IN, OUT and IN OUT to be used with any subprograms.

## USAGE of INOUT
```
--USING INOUT
DECLARE
  v_my_string VARCHAR2(100) := 'Hello';
  FUNCTION add_suffix (v_str IN OUT VARCHAR2, v_suffix IN VARCHAR2) RETURN VARCHAR2 IS
    BEGIN
      v_str:= v_str || v_suffix;
      RETURN v_str;
  END add_suffix;
BEGIN
  DBMS_OUTPUT.PUT_LINE('Before: ' || v_my_string);
  v_my_string := add_suffix(v_my_string, ', world!');
  DBMS_OUTPUT.PUT_LINE('After: ' || v_my_string);
END;
```
return 
Before: Hello
After: Hello, world!

## USAGE OF IN
```
--USING IN
DECLARE
  v_my_string VARCHAR2(100) := 'Hello';
  FUNCTION add_suffix (v_str IN VARCHAR2, v_suffix IN VARCHAR2) RETURN VARCHAR2 IS
    BEGIN
      v_str:= v_str || v_suffix;
      RETURN v_str;
  END add_suffix;
BEGIN
  DBMS_OUTPUT.PUT_LINE('Before: ' || v_my_string);
  v_my_string := add_suffix(v_my_string, ', world!');
  DBMS_OUTPUT.PUT_LINE('After: ' || v_my_string);
END;
```
return
giving error message that v_str cannot be modified / assigned as return value.
need to declare another variable to concat both string.

## USAGE OF OUT
```
--USING OUT
DECLARE
  v_my_string VARCHAR2(100) := 'Hello';
  FUNCTION add_suffix (v_str OUT VARCHAR2, v_suffix IN VARCHAR2) RETURN VARCHAR2 IS
    BEGIN
      v_str:= v_str || v_suffix;
      RETURN v_str;
  END add_suffix;
BEGIN
  DBMS_OUTPUT.PUT_LINE('Before: ' || v_my_string);
  v_my_string := add_suffix(v_my_string, ', world!');
  DBMS_OUTPUT.PUT_LINE('After: ' || v_my_string);
END;
```
return
Before: Hello
After: , world!
because Hello never passed into function as it is declared as output.

# Assignment for PROCEDURE
![alt text](https://raw.githubusercontent.com/muhk01/plsql_exercise/main/6.%20Procedure%20and%20Function/4f1e5bd4-07b4-4487-9b7d-bf61b2c0953c.png)
CREATE and INSERT Into Table.
```
--Procedure assignment
create table cust_charge(cno number(3) primary key, meter_no number(3) unique, prev_reading number(3), current_reading number(3), units number(5), bill_amount number(38));
insert into cust_charge values (89,100,300,800,0,0);
insert into cust_charge values (67,101,200,800,0,0);
insert into cust_charge values (90,200,100,800,0,0);
```

Create Local Procedure
```
DECLARE
  v_cno NUMBER := 89;
  PROCEDURE update_unit_and_bills(p_cno IN NUMBER) IS
    v_row CUST_CHARGE%ROWTYPE;
    v_bills_total NUMBER;
    u NUMBER;
    v_bills NUMBER:=0;
    v_extras NUMBER:=0;
  BEGIN
    SELECT * INTO v_row FROM CUST_CHARGE WHERE cno = p_cno;
    u := v_row.current_reading - v_row.prev_reading;
    FOR c IN 1..u LOOP
      IF c < 100 THEN 
        v_bills:=v_bills + 0.5;
      ELSE
        v_extras:=v_extras + 0.75;
      END IF;
    END LOOP;
    v_bills_total := v_bills + v_extras;
    DBMS_OUTPUT.PUT_LINE('id: '  ' Bills Total '  ' Unit ' || u);
    update cust_charge set units = u, bill_amount = v_bills_total where cno=p_cno;
  END update_unit_and_bills;
BEGIN
FOR rec IN (SELECT cno FROM CUST_CHARGE) LOOP
v_cno := rec.cno;
update_unit_and_bills(v_cno);
END LOOP;
END;
```
