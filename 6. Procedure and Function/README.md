# Types of Subprograms

PL/SQL has two types of subprograms:
Procedures and Functions

## Difference between Procedure and Function
![alt text](https://raw.githubusercontent.com/muhk01/plsql_exercise/main/6.%20Procedure%20and%20Function/2020-05-17_06-53-11-4b347fe12579a8bf9131f1874704f616.png)
## Local Subprograms
Such procedures and functions are local to the PL/SQL module, which contains it. They can be created in the declarative section of the PL/SQL module, local to the module. The local module can be called anywhere in the module’s execution section. Example Consider a procedure that accepts two numbers and return addition, subtraction, multiplication, and division of two numbers or in other words a procedure to return multiple values through arguments :
```
DECLARE
	A NUMBER;
	B NUMBER;
	C NUMBER;
	D NUMBER;
	E NUMBER;
	F NUMBER;
  PROCEDURE PROCESS( A IN NUMBER, B IN NUMBER, C OUT NUMBER, D OUT NUMBER, E OUT NUMBER, F OUT NUMBER) IS
  BEGIN
    C:=A+B;
    D:=A-B;
    E:=A*B;
    F:=A/B;
  END;
BEGIN
	A:=10;
	B:=5;
	PROCESS(A,B,C,D,E,F);
	DBMS_OUTPUT.PUT_LINE('ADDITION IS'||C);
	DBMS_OUTPUT.PUT_LINE('SUBTRACTION IS'||D);
	DBMS_OUTPUT.PUT_LINE('MUTIPLICATION IS'||E);
	DBMS_OUTPUT.PUT_LINE('DIVISION IS'||F);
END; 
```

## Stored Subprograms
A stored procedure or function is a named PL/SQL code block that has been compiled and stored in one of the Oracle engine’s systems tables. Stored Procedures and Functions are stored in the Oracle database. They are invoked or called by any the PL/SQL block that appears within an application.
Create stored Procedure
```
CREATE OR REPLACE PROCEDURE STORED_PROCESS( A IN NUMBER, B IN NUMBER, 
C OUT NUMBER, D OUT NUMBER, E OUT NUMBER, F OUT NUMBER) IS
BEGIN
	C:=A+B;
	D:=A-B;
	E:=A*B;
	F:=A/B;
END;
```
Calling Procedure Process
```
DECLARE
    A NUMBER;
    B NUMBER;
    C NUMBER;
    D NUMBER;
    E NUMBER;
    F NUMBER;
BEGIN
    A:=10;
    B:=5;
    STORED_PROCESS(A,B,C,D,E,F);
    DBMS_OUTPUT.PUT_LINE('ADDITION IS'||C);
    DBMS_OUTPUT.PUT_LINE('SUBTRACTION IS'||D);
    DBMS_OUTPUT.PUT_LINE('MUTIPLICATION IS'||E);
    DBMS_OUTPUT.PUT_LINE('DIVISION IS'||F);
END;
```
## Local Function
A function is a subprogram that computes a value. Functions and procedures are structured alike, except that functions have a **_RETURN_** clause.
Example of Local Function
```
DECLARE
	A NUMBER;
	B NUMBER;
	C NUMBER;
	FUNCTION ADDN ( A IN NUMBER, B IN NUMBER) RETURN NUMBER IS
	BEGIN
		C:=A+B;
		RETURN(C);
	END;
BEGIN
	A:=10;
	B:=5;
	C:=ADDN(A,B);
	DBMS_OUTPUT.PUT_LINE('ADDITION IS'||C);
END; 
```

## Stored Function
Example of Stored Function, create a stored Function
```
CREATE OR REPLACE FUNCTION ADDN( A IN NUMBER, B IN NUMBER) 
    RETURN NUMBER IS
    C NUMBER;
BEGIN
    C:=A+B;
    RETURN(C);
END;
```

After stored Function created we may Call from PL/SQL Block.
```
DECLARE
   A NUMBER;
   B NUMBER;
   C NUMBER;
BEGIN
   A:=10;
   B:=5;
   C:=ADDN(A,B);
   DBMS_OUTPUT.PUT_LINE('ADDITION IS'||C);
END; 
```
