# Database Introduction
My own collections of intro material to database, because it seems so hard to find good database learning material.

The final goal are the understanding to implement a simple database management system and good grasp of SQL syntax.

**1. Caltech CS121:** http://users.cms.caltech.edu/~donnie/cs121/

**Lecture 1: Terminologies.**

Database - organized collection of information.
 
DBMS - software that manages the database.

Kind of database, depends on amount of data being managed and type/frequency of operations being performed:

- OLTP: Online transaction processing (transaction orientated)

- OLAP: Online analytical processing (analysis oriented)

Data Models define how data is connected to each other and how they are processed and stored. Most db uses relational model.

Entity-Relationship Model:

- Useful for modelling abstraction at higher level than relational model 

- Easy to translate into relational model 

Relations: tables of data 

Attributes: each relation has some attributes (columns)

Domain: each attribute has a domain (set of valid values)

Superkeys: set of attributes that uniquely identifies tuples in a relation 

Candidate key: minimal super key 

Primary key: candidate key that's commonly used. List first in relation schema, and are underlined

Foreign key: One relation schema can cindlue the attributes of another schema's primary key

Referential integrity: two dependent relations is called referential integrity. Every foreign key must have a corresponding primary key value

**Lecture 2: Why Relational Algebra is useful, fundamental operations for database and additional operators.**

Query language: specified how to access data

2 kinds of query languages:

- Declarative: specify what data to retrieve, but not how 

- Procedural: specify what to retrieve as well as how 

Thanks to Kenny Song for discovery of the material

Relation Algebra: useful for providing the theoretical construct for the fundamental relational operations based on set theory and algebra 

6 fundamental operations:

- Select (sigma): include a predicate for selection 

- Project (capital pi): select the attributes in the output schema 

- Union: relations must have compatible schema (same arity, attributes have same domain)

- Different (-): relations must have compatible schema 

- Cartesian product: no constrain on schema. Output schema is concatenation of input schemas. Distinguish overlapping attributes names by prepending the source relation's name

- rename (rho): does not create a new relation-variable 

Additional operations:

- Set intersection

- Natural join: join relations on common attributes 

- Division: for each type of query. R divides S: find all rows in R that have one row corresponding to each row in S. Output schema is R - S

- Assignment: persists, unlike rename operations 

**Lecture 3: More advanced operations.**

Generalized projection: generate result that doesn't appear as an attribute in the original relation

Aggregate function: sum, avg, count, min, max (-distinct)

Grouping and Aggregation: group then perform aggregate 

Outer join: left, right, full (padding missing values as null) 

Each relational operation has different behavior with respect to null

Constant relation can be used to add new tuple to relation 

Update: usually use generalized projection 

Summary: relationship algebra is procedural and verbose, useful because it can be reasoned about 

**Lecture 4: Basic SQL syntax.**

Mainly declarative

2 parts:

- Data Definition Language (DDL). Schema and constrains

- Data Manipulation Language (DML). Querying

SQL language is case-insensitive. 

USE db_name: make db_name default database for current connection 

CREATE: CREATE TABLE t_name {
  attr1 domain1,
  attr2 domain2,
  ...
  PRIMARY KEY (attr1, attr2, ...)
}

Common domain types: CHAR(N), VARCHAR(N), INT, NUMERIC(P, D), DOUBLE PRECISION (an approximation), FLOAT(N), DATE, TIME, TIMESTAMP, BLOB, CLOB, TEXT

INSERT INTO db_name (col_names)? VALUES (value1, value2, ...). Can specify which attributes in INSERT.

DELETE FROM t_name WHERE? ...;

DROP TABLE - DROP DATABASE 

SELECT attr1, attr2, ... FROM table1, table2, ... WHERE ...;

- relations are multisets, duplicates remain

- Can rename attribute, table_name with AS 

- Use LIKE for pattern matching in WHERE 

- If tables have overlapping attr, use t_name.attr_name to distinguish 

Set operations:

- select1 UNION select2 

- select1 INTERSECT select2

- select1 EXCEPT select2 

- Eliminates duplicates. Can keep duplicates by appending ALL to the set operations 

*? means optional

**Lecture 5. SQL Queries.**

General form is SELECT attr1, attr2, ... FROM table1, table2, ... WHERE P

ORDER BY at the end of SELECT statement to order by attribute 

Grouping & Aggregate functions in SQL (SUM, AVG, COUNT, MIN, MAX)

- e.g. SELEcT AVG(balance) FROM account WHERE branch_name = 'New York'

- SELECT attr1, attr2, ... , F1, F2, ... FROM t1, t2, ... WHERE P GROUP BY attr1, attr2, ... Notice the grouping attributes appear type. If the group attributes do not appear immediately after SELECT, they won't be in schema. 

- WHERE clause is applied before any group occurs. To apply filter after grouping, use HAVING.

- Use DISTINCT to eliminate duplicates 

- COUNT(\*) counts total number of tuples, do not ignore NULL. To ignore NULL, use COUNT(attr)

Nested subqueries

- A single query can only perform 1 agg function 

- Scalar subquery: one attr and one tuple, automatically unpack value when compared against

Subqueries in WHERE and HAVING clause

- Set membership test: IN, NOT IN (less freq: ANY, SOME, ALL)

- Empty set test: EXISTS, NOT EXISTS 

- Uniqueness test: UNIQUE, NOT UNIQUE 

Correlated queries: when a nested query refers to the enclosing query's attributes. Slow and sometimes decorrelated automatically by database. Avoid if performance suffers.

Subqueries in FROM Clause:

- Used to compute a result in multiple steps. Query against a subquery's result (called a derived relation)

- Subquery in FROM clause must be given a name

More Data Manipulation Operation:

- INSERT INTO table ... VALUES / SELECTED ... 

- DELETE FROM table WHERE? ...

- UPDATE table SET attr1=val1, attr2=val2, ... WHERE P
