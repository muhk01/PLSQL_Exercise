
# Usage of TRIGGER To UPPERCASE the INSERTED String
For each execution into emp_salary on emp_name table for each record will be automatically UPPERCASED.
```
CREATE OR REPLACE TRIGGER emp_upper
BEFORE INSERT OR UPDATE OF emp_name
ON emp_salary
FOR EACH ROW
BEGIN
    :new.emp_name:= UPPER(:new.emp_name);
END;
```

# Usage of TRIGGER to Print old and New Values Each record Updated
```
--TRIGGER TO SHOW OLD AND NEW VALUE ENAME EVERY UPDATE
CREATE OR REPLACE TRIGGER emp_update
BEFORE UPDATE OF emp_name
ON emp_salary
FOR EACH ROW
BEGIN
    DBMS_OUTPUT.PUT_LINE('Old Name : ' || :old.emp_name);
    DBMS_OUTPUT.PUT_LINE('New Name : ' || :new.emp_name);
END;
```

# Trigger to update another table2 each Insertion on Table1
```
CREATE OR REPLACE TRIGGER trg_insert_example
AFTER INSERT ON table1
FOR EACH ROW
BEGIN
  UPDATE table2
  SET column2 = :NEW.column1
  WHERE table2.id = :NEW.id;
END;
```

# TRIGGER to prevent INSERTION on Spesific Statement
```
CREATE OR REPLACE TRIGGER trg_prevent_insertion
BEFORE INSERT ON your_table
FOR EACH ROW
DECLARE
  l_condition BOOLEAN;
BEGIN
  -- Check the condition that should prevent insertion
  -- In this example, we're checking if the inserted value for column1 is 'XYZ'
  IF :NEW.column1 = 'XYZ' THEN
    l_condition := TRUE;
  ELSE
    l_condition := FALSE;
  END IF;

  -- If the condition is true, raise an exception to prevent insertion
  IF l_condition THEN
    RAISE_APPLICATION_ERROR(-20001, 'Insertion not allowed for column1 value = ''XYZ''');
  END IF;
END;
```
Suppose we call INSERTION STATEMENT :
```
INSERT INTO your_table VALUES ('abc', 'Test1')
INSERT INTO your_table VALUES ('xyz', 'Test2')
```
The result will not inserted because when condition meets the TRIGGER will automatically RAISE_APPLICATION_ERROR
```
column1 | column2
--------+--------
abc     | Test1
```
Suppose we want to Update certain emp_no it will print both before and after updated value
```
UPDATE C##usernew.emp_salary SET emp_name='raj' WHERE emp_no=1;
```
#### Noted for FOR EACH usage
In PL/SQL triggers, the "FOR EACH ROW" clause determines whether the trigger is executed once for each row affected by the triggering statement or only once for the entire statement. Here's a breakdown of when to use "FOR EACH ROW" and when not to use it:

Use "FOR EACH ROW":

When you need to perform some action for each individual row affected by the triggering statement. For example, if you want to update a column in another table for each inserted/updated/deleted row.
When you want to refer to the values of the affected row(s) using the "OLD" and "NEW" qualifiers. These qualifiers allow you to access the old and new values of the row being modified.
Don't use "FOR EACH ROW":

When you want the trigger to execute only once for the entire triggering statement, regardless of the number of rows affected. This is useful when you want to perform an action based on the overall result of the statement, rather than on individual rows.
When the trigger doesn't require access to the old and new values of the row being modified. If your trigger doesn't need to reference these values, you can omit the "FOR EACH ROW" clause to improve performance.
