# Control Statements

We can change the logical flow of statements within the PL/SQL block with a number of control structures.
![alt text](https://raw.githubusercontent.com/muhk01/plsql_exercise/main/3.%20Loop%20and%20Conditional%20Statements/2020-05-16_06-51-49-854e682a6fe66e31cd460ad58f6ef34e.png)

## Conditional Control
It allows testing the truth of a condition and executing sections of the program depending on the condition that may be true or false.

### IF Statements
There are three forms of IF statements: IF-THEN, IF-THEN-ELSE, and IF-THEN-ELSIF.
#### IF-THEN
The simplest form of IF statement associates a condition with a sequence of statements enclosed by the keywords THEN and END IF (not ENDIF)
Example :
```
IF a > b THEN
   dbms_ouput.put_line('a is greater'); 
END IF;
```

#### IF-THEN-ELSE
The second form of IF statement adds the keyword ELSE followed by an alternative sequence of statements. Example :
```
DECLARE
   A NUMBER := 10;
   B NUMBER := 20;
BEGIN
   IF A > B THEN  
      DBMS_OUTPUT.PUT_LINE('A IS GREATER');
   ELSE
      DBMS_OUTPUT.PUT_LINE('B IS GREATER');
   END IF;
END;
```

Additional example IF-THEN nested, suppose to compare number from declared variables.

```
DECLARE
     A NUMBER := 10;
     B NUMBER := 20;
     C NUMBER := 30;
BEGIN
IF A>B THEN
   IF A>C THEN 
       DBMS_OUTPUT.PUT_LINE('A IS GREATEST');
   ELSE
       DBMS_OUTPUT.PUT_LINE('C IS GREATEST');
   END IF;
ELSE
   IF B>C THEN
       DBMS_OUTPUT.PUT_LINE('B IS GREATEST');
   ELSE
       DBMS_OUTPUT.PUT_LINE('C IS GREATEST');
   END IF;
END IF;
END;
```

#### IF-THEN-ELSIF
Sometimes we want to select an action from several mutually exclusive alternatives.
The third form of IF statement uses the keyword ELSIF with additional spesific condition, so instead using ELSE we using ELSIF with other spesific criteria.
```
declare
a number:=1;
b number:=1;
c number;
d number;
begin
c:=3;
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
end if;
DBMS_OUTPUT.PUT_LINE('c is equal : ' || c);
end;
```


## Iterative Control
It allows executing a section of the program repeatedly as long as a specified condition remains true.
The LOOP command initializes a group of commands indefinitely, or until a condition forces a “break” in the LOOP and detours the execution of the program to another place. The command is used with the EXIT command, which is responsible for interrupting the LOOP execution.

### Simple LOOP Statement
The simplest form of LOOP statement is the basic (or infinite) loop, which encloses a sequence of statements between the keywords LOOP and END LOOP,  If further processing is undesirable or impossible, you can use an EXIT statement to complete the loop using EXIT or EXIT WHEN.

#### EXIT Statement
The EXIT statement forces a loop to complete unconditionally. When an EXIT statement is encountered, the loop completes immediately and control passes to the next statement. Example :
```
LOOP
...
IF credit_rating < 3 THEN
   ...
   EXIT; -- exit loop immediately
   END IF;
END LOOP;
-- control resumes here
```

#### EXIT-WHEN Statement
The EXIT-WHEN statement allows a loop to complete conditionally. When the EXIT statement is encountered, the condition in the WHEN clause is evaluated.


## Sequential Control
It allows ordering the sequence of processing sections of the program.
```
LOOP 
      EXIT WHEN c>5;  -- exit loop if condition is true
   ...
END LOOP;
```

