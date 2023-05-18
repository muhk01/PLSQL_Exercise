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

## Usage GOTO to skip to End Statement when no number Doesn't Satisfy the Assigned Value.
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
