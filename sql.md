## SQL

[Concepts](#the-relational-model)  
[Syntax](#sql-syntax)  

### The Relational Model  
*Notes from Stanford Mini Course*  

##### Database
>A set of named **relations** (or **tables**)  
Each relation has a set of named **attributes** (or **columns**)  
Each **tuple** (or **row**) has a value for each attributes  
Each Attribute has a **type** (or **domain**)  

**NULL** - special value for "unknown" or "undefined"

**Key** - attribute whose value is unique in each tuple  
or set of attributes whose combined values are unique

Steps in creating and using a Relational Database
1. Design schema; create using DDL
2. "Bulk load" initial data
3. Repeat: execute queries and modifications

**Compositionality** - ability to run a query over results of another query

**CRUD** - Create, Read, Update, Delete

### SQL Syntax  

Use wildcard to select all
```SQL
SELECT *
FROM table_name
```
AND / OR
```SQL
SELECT column_name(s)
FROM table_name
WHERE condition
AND|OR condition
```
DELETE
```SQL
DELETE FROM table_name
WHERE some_column=some_value  /* targeted delete */

DELETE FROM table_name  /* deletes the entire table! */

DELETE * FROM table_name  /* deletes the entire table! */
```
