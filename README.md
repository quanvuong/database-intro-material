# Database Introduction
My own collections of intro material to database, because it seems so hard to find good database learning material.

The final goal are the understanding to implement a simple database management system and good grasp of SQL syntax.

1. Caltech CS121: http://users.cms.caltech.edu/~donnie/cs121/

Lecture 1: Terminologies.

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

Lecture 2: Why Relational Algebra is useful, fundamental operations for database and additional operators. 

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

 
