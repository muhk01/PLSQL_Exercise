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
```
LOOP 
      EXIT WHEN c>5;  -- exit loop if condition is true
   ...
END LOOP;
```

### WHILE-LOOP Statement
The WHILE-LOOP statement associates a condition with a sequence of statements enclosed by the keywords LOOP and END LOOP. Before each iteration of the loop, the condition is evaluated. If the condition yields TRUE, the sequence of statements is executed, then control resumes at the top of the loop.
```
WHILE i <= 10 LOOP
  a:=n*i;
   i:=i+1;
END LOOP;
```

### FOR LOOP Statement

Whereas the number of iterations through a WHILE loop is unknown until the loop completes, the number of iterations through a FOR loop is known before the loop is entered. FOR loops iterate over a specified range of integers.
The range is evaluated when the FOR loop is first entered and is never re-evaluated. As the next example shows, the sequence of statements is executed once for each integer in the range. After each iteration, the loop counter is incremented.
```
FOR i IN 1..3 LOOP  -- assign the values 1,2,3 to I
   sequence_of_statements;  -- executes three times
END LOOP;
```

## Sequential Control
It allows ordering the sequence of processing sections of the program.

### GOTO Statement
The GOTO statement branches to a label unconditionally. The label must be unique within its scope and must precede an executable statement or a PL/SQL block.
for every <<GOTO>> should followed with some statement, here example of illegal GOTO Statement
```
LOOP
…….
IF A>B then
    Go to <<abc>>;
END IF;
……
    <<abc> -- it is illegal because it does not precede the executable statement.
  END LOOP:
End;
```
The solution of illegal use of GOTO statement is with the NULL statement as shown below:
```
LOOP
….,…
 IF A>B THEN
    GO TO <<ABC>>;
  END IF;
  …….
  <<abc>> /* It is correct now because it is followed by an executable 
           statement  NULL without changing the meaning of the block.*/
  NULL;
END LOOP;   
```
