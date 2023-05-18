# Intro PLSQL
PL/SQL stands for Procedural Language/Structured Query Language. PL/SQL is an extension of the SQL language. We can say it is the superset of the Structured Query Language specialized for use in the Oracle database.

# SQL Vs PL/SQL
SQL does not have any procedural capabilities. By procedural capabilities here we mean that there is no provision of conditional checking, looping and branching, which are very essential for filtration of data before entering it into the database. In SQL there is no provision of handling errors and exceptions, which means that if any SQL statement fails to execute, then oracle gives its own error messages and error code which may not be user friendly.

# Advantage of PLSQL
Supports the declaration and manipulation of object types and collections. Allows the calling of external functions and procedures. Contains new libraries of built-in packages. A package is a file that group functions, cursors, stored procedures, and variables in one place.
Triggers: A trigger is a PL/SQL program that is stored in the database and executed immediately before or after the INSERT, UPDATE, and DELETE commands.
Cursors: Oracle uses workspaces to execute the SQL commands. Through PL/SQL cursors, it is possible to name the workspace and access its information.

# Structure of PL/SQL Language
PL/SQL is a block-structured language with procedural techniques with features like logic building, looping, error-handling mechanisms, data-types, variables, subroutines, procedural constructs. Block is the smallest piece of PL/SQL code which groups logically related declarations and statements. Declarations are local to the blocks and cease to exist when the block completes.
PL/SQL block consists of three sections:
A PL/SQL statement is terminated with the END statement and a semicolon. 
Every PL/SQL program must consist of at least one block, which may contain any number of nested sub-blocks.
Blocks can be nested in executable and exception-handling parts of a PL/SQL block or subprogram but not in declarative part.
