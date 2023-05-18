# Types of Subprograms

PL/SQL has two types of subprograms:
Procedures
Functions

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
