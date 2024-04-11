### Lecture 1 - 28 Feb 24

Database
Organized Collection of interrelated data that models some aspect of the real-world

CSV File
- Comma Separated Value
- Problems
	- Integrity: Is the data reliable?
	- Implementation: How to make this system?
	- Durability: Is it safe to use this?

Solution: DataBase Management Systems(DBMS)
- information about particular enterprise
	- collection of interrelated data
	- set of programs to access data
	- convenient and efficient to use

Disadvantages of database applications on file systems(not DBMS)
- Data redundancy and inconsistency
- Hard accessing data
- Multiple formats
- Hard to make data reliable(many constraints)
- Updates should be done or not done at all
- Concurrent actions are hard
- Security

#### Data Models
Collection of tools for describing data, relationships, semantics, constraints
- Relational mode
- Entity-Relationship data model
- Object-baed data model
- Semi-structured data model

##### Relational Model
All data is stored in various tables
![[Pasted image 20240228150423.png|400]]

Levels of abstraction
![[Pasted image 20240228150814.png|200]]
Physical level: describing how record is stored(physically stored in the storage) - people who uses the data base does not need to know this
Logical level: describing data in database & relationships in data(The whole data)
View label: parts of actual database - can hide salary to people using data
![[Pasted image 20240228150927.png|500]]![[Pasted image 20240228151554.png|300]]
Logical Schema: overall logical structure of database
Physical Schema: overall physical structure of database

##### Physical Data Independence
Ability to change physical schema without changing logical schema
- Applications depend on logical schema - should not change user application

##### Data Definition Language(DDL)
- Syntax to create & change objects like tables, indices, users
- Data dictionary contains metadata(data about data)

##### Data Manipulation Language(DML)
For Adding, Deleting, modifying data
- Procedural DML:  what data is needed and how to get it
- Declarative DML: what data is needed but does not provide how to get it

##### SQL
- Non-procedural: input several tables and always returns single table
- Compute complex functions - embedded in higher level language

### Database Design - 04 Mar 24

Database design: Designing the general structure of database
- Logical design: maps the high-level conceptual schema onto the implementation data model of the database system that will be used
- Physical design: physical features of the database are specified

Storage Manager(close to database)
Interface between the low-level data stored in the database and the application programs and queries submitted to the system

__Query Processor(close to user)__
Module that processes requests received from the user
- DDL interpreter: interpret DDL statement, record definitions
- DML compiler: translate DML statement in query language to evaluation plan(low-level instructions)
- Query evaluation engine: executes low-level instructions
![[Pasted image 20240304144617.png|500]]

__Query processing__
- Parsing & translation
- Optimization
- Evaluation
![[Pasted image 20240304144751.png|400]]
For optimizing, we need statistics about data

__Transaction Management__
Transaction: Collection of operation that performs single logical function in database application, unit of atomicity, consistency.
Transaction manager
- Concurrency-control manager: control interaction among concurrent transactions
- Recovery manager: Has to do failure recovery(If transaction fails we need to ensure it has no effect on state of database)

__Database Architecture__
![[Pasted image 20240304145636.png|500]]
Two tier vs Three tier Architectures
![[Pasted image 20240304150133.png|400]]
Difference
- Three-tier provide better security & performance
- Application server business logic: what actions to carry out on specific conditions
	- Two-tier: logic is distributed across multiple clients
	- But application server is expensive

__Database Users & Administrators__
Types of users
- Naive users: using predefined user interfaces
- Applications programmers: Who write application programs
- Sophisticated users: interact with system without programming. Form requests using database query language, data analysis software
Database Administrator: Person who has central control over the system
- Schema definition
- Storage structure and access-method definition
- Schema & physical-organization modification
- Grating authorization for data access
- Routine maintenance

### Relational Model
Relational database consists of collection of tables each assigned an unique name
![[Pasted image 20240304153451.png|300]]
Instructor table - instructor relation

In relational model
- Relation: refer to a table, set of tuples $\rightarrow$ order of tuple is irrelevant
- Tuple: refer to a row
- Attribute: refer to a column
- Relation instance: specific set of rows
- Domain(of attribute): set of permitted values
	- Domain is atomic if elements of domain are indivisible units(cannot be separated into multiple units)

__Database Schema__
Database schema: logical design of database
Database instance: snapshot of data in database at one time
relation schema: type definition

__Keys__
Attribute values in tuple must be able to uniquely identified - no same tuple
Superkey: set of one or more attribute that allow us to identify uniquely a tuple in relation
Candidate key: Superkeys that does not have proper subsets as superkeys(minimal superkey)
Primary key: Candidate key that is chosen by the database designer
Foreign-key constraint
from attribute $A$ of relation $r_1$ to primary-key $B$ of relation $r_2$ states that on any database instance, the value $A$ for each tuple in $r_1$ must also be the value of $B$ for some tuple in $r_2$

__Schema Diagrams__
- Relation: box
- Primary key: underlined
- foreign-key constraints: arrows from the foreign-key attributes of the referencing relation to the primary key of the referenced relation
- two-headed arrow: referential integrity constraint
![[Pasted image 20240306152650.png]]

__Relational Query Languages__
Query Langauage
- Language which a user requests information from the database
	- Imperative
	- Functional
	- Declarative
	- 