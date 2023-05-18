# Data types and Declaration

Every constant and variable has a data type, which specifies a storage format, constraints, and valid range of values.
Some commonly used data types of PL/SQL are:
```
NUMBER
CHAR
VARCHAR
DATE
BOOLEAN
LONG
LONG RAW
LOB
```

# Operators, Indicators and Punctuation

In PL/SQL, these symbols are divided into a few groups:

## Arithmetic operators
Used to perform arithmetic operations.
Examples: +, -, *, /, ** (Raises the first operand to the exponent of the second)
```
SUM:= NUMBER1 + NUMBER2;
```

## Expression operators
Used to create an assignment, range, and string catenation expressions.
Examples:=(Assignment operator on declaration)
```
A NUMBER(3):=3
```

# Comments

Comments can be a single line or multiple lines.
## Single line comment:
Begins with -- can appear within a statement, at end of the line.
Example :
```
a number;--the variable declaration
```
## Multi-line comment :
Begin with /* and end with an asterisk slash (*/).
Example :
```
/* statements to select rate and quantity into
variables and calculate value */
```

# Variables and Constants
The PL/SQL language allows the declaration of variables and constants, which can be used in the SQL commands contained in the PL/SQL block. All the variables and constants used must be declared.

## Variables
We can declare variables in the declaration section part and use elsewhere in the body of a PL/SQL block. The following example shows how to declare a variable
Example :
```
age number (4);
```

## With the use of SELECT INTO clause
The second way to assign values to variables is to use the SELECT command to assign the contents of the fields of a table to a variable:
```
SELECT sal INTO s FROM emp where empno = 100;
```
In this case, variables’ will get the value from sal column of emp table for empno 100.

## Constant Declaration

The declaration of a constant is similar to that of the declaration of a variable. We can declare constants in the declaration section and use it elsewhere in the executable part. To declare the constant we must make use of the keyword constant. This keyword must precede the data type as shown below.
```
pi constant number : = 3.14;
```

## Variable Attributes
Attributes allow us to refer to data types and objects from the database. PL/SQL variables and constants can have attributes. The following are the types of attributes, which are supported by PL/SQL.
¨ %TYPE
¨ %ROWTYPE

### %TYPE
In general, the variables that deal with table columns should have the same data type and length as the column itself. %type attribute is used when declaring variables that refer to the database columns. When using the %type keyword, all you need to know is the name of the column and the table to which the variable will correspond.
