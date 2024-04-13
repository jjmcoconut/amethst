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


# 1. Introduction
- **Definition:** Collection of interrelated data with programs to access it.
- **Purpose:** Efficiently store and retrieve data for enterprises, ensuring safety and preventing anomalies.

## 1.1 Database-System Applications 
- **Evolution:** From simple commercial data management to complex, global enterprises.
- **Common Elements:** Data centrality, crucial for modern corporations' value and functionality.

__Abstraction and Complexity Management__
- **Abstraction:** Simplifies complex systems for user interaction.
- **Database Systems:** Provide a unified view of data, managing complexity effectively.

__Representative Applications__
- **Enterprise Information:** Sales, Accounting, Human Resources, Manufacturing.
- **Banking and Finance:** Banking, Credit Card Transactions, Finance.
- **Other Sectors:** Universities, Airlines, Telecommunication, Web-based services, Document databases, Navigation systems.

__User Interaction with Databases__
- **Evolution:** From back-office systems to direct customer interactions via web and mobile applications.
- **Usage:** Nearly every interaction with modern technology involves accessing databases.

__Modes of Database Usage__
1. **Online Transaction Processing:** Many users, small data retrieval and updates.
2. **Data Analytics:** Processing data for drawing conclusions, driving business decisions.

__Data Analytics in Practice__
- **Examples:** Loan approvals, Advertisement targeting, Manufacturing and Retail decisions.
- **Techniques:** Data mining combines knowledge discovery and statistical analysis on large databases.

## 1.2 **Purpose of Database Systems**

In a university organization, managing information about instructors, students, departments, and courses is crucial. Traditional file-based systems store this data with application programs to manipulate it. However, this approach faces several challenges:

1. **Data Redundancy and Inconsistency:** Different file structures and programming languages lead to duplicated data and inconsistencies.
2. **Difficulty in Accessing Data:** Retrieving specific data requires custom application programs, leading to inefficiency.
3. **Data Isolation:** Scattered data in various formats make developing new applications challenging.
4. **Integrity Problems:** Enforcing consistency constraints across different files is complex.
5. **Atomicity Problems:** Ensuring all or nothing transactions in case of system failures is difficult.
6. **Concurrent-Access Anomalies:** Simultaneous data updates may result in inconsistent states.
7. **Security Problems:** Enforcing access control is cumbersome due to ad hoc application additions.

These challenges drove the development of database systems in the 1960s and 1970s. Database systems address these issues through concepts and algorithms, providing efficient and secure data management solutions.

## 1.3 **View of Data**

### 1.3.1 Data Models
- A **database system** consists of interrelated data and programs for accessing and modifying them.
- **Data model:** Conceptual tools for describing data, relationships, semantics, and consistency constraints.
- Four categories of data models:
  - **Relational Model:** Uses tables to represent data and relationships, widely used in current systems.
  - **Entity-Relationship Model:** Utilizes entities and relationships among them.
  - **Semi-structured Data Model:** Allows data with varying attributes, like JSON and XML.
  - **Object-Based Data Model:** Integrates object-oriented concepts into databases, often used with Java, C++, or C#.

### 1.3.2 Relational Data Model
- Data represented in tables with multiple columns.
- Each row represents one piece of information.
- Illustration with sample university instructors and department details.

### 1.3.3 Data Abstraction
- **Efficient data retrieval** requires complex structures, abstracted for user simplicity.
- Levels of abstraction:
  - **Physical level:** Describes actual data storage.
  - **Logical level:** Describes stored data and relationships, offering physical data independence.
  - **View level:** Presents only relevant portions of the database to users, providing simplified interaction.

### 1.3.4 Instances and Schemas
- **Instances:** Collection of stored information at a specific moment.
- **Schemas:** Overall database design.
- Partitioned into physical, logical, and view schemas.
- **Logical schema** crucial for application development, offering physical data independence.
- Need for well-designed schemas to avoid issues like redundant information.

*Note: Emphasizing key concepts and categorizing data models and abstraction levels.*

## 1.4 **Database Languages**

A **database system** includes a **data-definition language (DDL)** for schema specification and a **data-manipulation language (DML)** for queries and updates. These are often parts of a unified language like **SQL**. Integrity constraints, such as **domain constraints** and **referential integrity**, ensure data consistency. **Authorization** controls user access levels. DDL statements generate output stored in a **data dictionary**, containing metadata.

**The SQL Data-Definition Language**

SQL's rich DDL defines tables and integrity constraints. For instance, a SQL statement defines a **department table** with specific columns and types. SQL supports primary keys and referential integrity, ensuring data consistency.

**Data-Manipulation Language**

**DMLs** enable data retrieval, insertion, deletion, and modification. Procedural DMLs specify data retrieval methods, while declarative DMLs focus on what data is needed without specifying retrieval methods. Queries, a subset of DML, request data retrieval. SQL, a nonprocedural language, is widely used for querying.

**Database Access from Application Programs**

SQL, not as powerful as general-purpose languages, requires embedded queries in host languages like C/C++, Java, or Python. Application programs interact with databases for various tasks like student registration, GPA calculation, etc. DML and DDL statements are sent to the database using APIs like **ODBC** or **JDBC**.

## 1.5 **Database Design**

Database systems manage large bodies of information within enterprises. The design process mainly focuses on **database schema**. Understanding user requirements is crucial, followed by choosing a **data model** and translating requirements into a **conceptual schema**. This schema defines data relationships and ensures satisfaction of functional requirements.

In relational model context, decisions involve selecting attributes and grouping them into tables. The process can employ either the **entity-relationship model** or **normalization algorithms**.

Moving from abstract to implementation involves logical design, mapping the conceptual schema to the system-specific data model, and then the physical design, specifying storage structures.

## 1.6 Database Engine

The database system comprises modules: storage manager, query processor, and transaction management. 

- **Storage Manager:** Interfaces between low-level data and applications, includes components like authorization, transaction, file, and buffer managers.
- **Query Processor:** Includes DDL interpreter, DML compiler, and query evaluation engine. Translates DML statements into low-level instructions and executes them.
- **Transaction Management:** Ensures atomicity, consistency, isolation, and durability (ACID properties) of database transactions. Manages concurrent access to data and system failures.

Modern database engines emphasize **parallel processing** for handling large data efficiently and often utilize **solid-state disks (SSDs)** for faster storage.

For detailed reading:
- Database Design: Chapters 6 and 7
- Database Engine: Chapters 12, 13, 14, 15, 16
- Transaction Management: Chapters 17, 18, 19

## 1.7 Database and Application Architecture

The architecture of a centralized database system is depicted in Figure 1.3, illustrating user interaction and database engine components. This centralized structure suits shared-memory server setups, but for larger data volumes and higher speeds, parallel and distributed databases are utilized. Chapters 20 through 23 explore system structures, query processing, transaction processing, and maintenance in these contexts.

Modern database applications exhibit either two-tier or three-tier architecture, as shown in Figure 1.4. Traditional two-tier setups involve client-side applications interacting directly with server-side databases. Conversely, contemporary three-tier configurations separate the client, application server, and database, enhancing security and performance.

## 1.8 Database Users and Administrators

Database system users fall into four categories: Naive users, Application programmers, Sophisticated users, and Database Administrators (DBAs). Each interacts with the system differently, utilizing distinct user interfaces.

DBAs play a crucial role in database management, overseeing schema definition, storage structure, user authorization, and routine maintenance tasks.

## 1.9 History of Database Systems

- **1950s-1970s:** Evolution from punched cards to magnetic tapes, then hard disks. Relational model introduced by Edgar Codd in 1970.
- **Late 1970s-1980s:** Commercialization of relational databases, including IBM's System R and Oracle.
- **1990s:** Emergence of decision support applications, parallel databases, and object-relational features. Growth of the World Wide Web impacts database usage.
- **2000s:** Evolution of data storage formats (XML, JSON), growth of open-source databases, and development of graph databases.
- **2010s:** Rise of NoSQL systems, outsourcing of data management to cloud services, and increased focus on data security and privacy regulations.

# 2. Introduction to the Relational Model

- **Importance:** Relational model is primary for commercial data-processing due to its simplicity, evolving over 50 years with object-relational features, XML support, and tools for semi-structured data.
- **Chapter Focus:** Fundamentals, database theory, relational schema design, query processing efficiency, and formal relational languages.

## 2.1 Structure of Relational Databases

- **Table Collection:** Relational databases comprise tables, each uniquely named.
- **Example:** Tables like 'instructor' and 'course' contain rows with corresponding attributes.
- **Row Representation:** Each row represents a relationship among values, akin to tuples in mathematical relations.
- **Terminology:** Relation refers to a table, tuple to a row, and attribute to a column.
- **Instance:** Specific set of rows in a relation.
- **Attribute Domain:** Permitted values for each attribute, ensuring atomicity.

**Atomicity and Null Values**

- **Atomic Domains:** All attribute domains must be atomic, treating elements as indivisible.
- **Null Value:** Signifies unknown or nonexistent value, posing challenges in database operations.
- **Elimination:** Preferably avoid null values due to operational difficulties.

**Practical Advantages and Limitations**

- **Advantages:** Strict relational structure aids in data storage and processing efficiencies.
- **Limitations:** Less suitable for dynamic applications where data and structure change over time.

*Note: Detailed discussions on relational theory, schema design, and database operations are provided in subsequent chapters.*

## 2.2 **Database Schema**

When discussing a database, we distinguish between the **database schema** (logical design) and the **database instance** (snapshot of data at a specific time). A **relation** corresponds to a variable, while a **relation schema** is akin to a type definition in programming. It consists of attributes and domains.

- **Relation Instance:** Comparable to the value of a variable, it may change over time.
- **Relation Schema:** Attributes and domains, usually static.

For simplicity, the same name (e.g., "instructor") is often used for both schema and instance, though explicit differentiation is possible. Common attributes in schemas facilitate relating tuples across different relations.

Consider the "department" relation schema: department (dept name, building, budget). Shared attributes like "dept_name" facilitate data retrieval across related relations.

A university database might include various relations:

- **section:** Describing class offerings (course id, sec id, semester, year, building, room number, time slot id).
- **teaches:** Associating instructors with class sections they teach (ID, course id, sec id, semester, year).

Additional relations in a university database include:

- **student:** Records student information (ID, name, dept_name, total_credit).
- **advisor:** Associates students with their advisors (s id, i id).
- **takes:** Tracks student enrollment in courses (ID, course id, sec id, semester, year, grade).
- **classroom:** Details about classrooms (building, room number, capacity).
- **time slot:** Information about time slots for classes (time slot id, day, start_time, end_time).

*Note: SQL queries for creating these tables would depend on the specific database management system being used.*

## 2.3 Keys

- **Distinguishing Tuples:** Attributes must uniquely identify tuples within a relation.
- **Superkey:** Set of attributes allowing unique tuple identification.
- **Candidate Key:** Minimal superkey; no proper subset is a superkey.
- **Primary Key:** Chosen key for tuple identification; a candidate key designated by the database designer.
- **Primary Key Constraint:** Prohibits identical key attribute values in different tuples.
- **Underlining:** Indicates primary key attributes in a relation schema.
- **Foreign-Key Constraint:** Ensures values in one relation's attribute(s) correspond to the primary key of another relation.
- **Referential-Integrity Constraint:** Requires values in specified attributes of one relation to appear in specified attributes of another relation.
- **Foreign Key:** Attribute(s) in one relation referencing the primary key of another relation.
- **Referencing Relation:** Contains the foreign key(s).
- **Referenced Relation:** Contains the primary key referenced by the foreign key.
- **Generalization:** Referential-integrity constraints relax the requirement that referenced attributes must form the primary key.
- **Support:** Database systems typically support foreign-key constraints but not referential integrity constraints where the referenced attribute is not a primary key.

```sql
-- SQL to create a table with primary key
CREATE TABLE classroom (
    building VARCHAR(50),
    room_number INT,
    capacity INT,
    PRIMARY KEY (building, room_number)
);

-- SQL to create a table with foreign key constraint
CREATE TABLE instructor (
    ID INT PRIMARY KEY,
    name VARCHAR(50),
    dept_name VARCHAR(50),
    FOREIGN KEY (dept_name) REFERENCES department(dept_name)
);
```

## 2.4 **Schema Diagrams**

A **database schema** is represented with schema diagrams, incorporating **primary key** and **foreign key** constraints. Each relation is depicted as a box with the relation name highlighted in blue at the top, and attributes listed inside. Primary key attributes are underlined, while foreign key constraints are indicated with arrows from referencing attributes to the primary key of referenced relations. Two-headed arrows denote referential integrity constraints distinct from foreign key constraints. 

*Figure 2.9* illustrates this with a two-headed arrow from 'time slot id' in the 'section' relation to 'time slot id' in the 'time slot' relation, symbolizing the referential integrity constraint between them. While many database systems offer graphical tools for creating such diagrams, another representation called the **entity-relationship diagram** will be discussed later in Chapter 6.

## 2.5 **Relational Query Languages**

A **query language** facilitates user requests from the database and typically operates at a higher level than standard programming languages. These languages fall into categories: imperative, functional, or declarative.

- **Imperative:** Instructs the system with a sequence of operations, often involving state variables.
- **Functional:** Expresses computation as the evaluation of functions without side effects.
- **Declarative:** Describes desired information without specifying steps, often using mathematical logic.

"Pure" query languages include:
- **Relational algebra:** Functional in nature, forming the theoretical basis of SQL.
- **Tuple relational calculus** and **domain relational calculus:** Declarative approaches described in Chapter 27.

While these languages lack the "syntactic sugar" of commercial languages, they illustrate fundamental data extraction techniques. Practical query languages, like SQL, blend elements from imperative, functional, and declarative paradigms. SQL, extensively used, will be covered from Chapter 3 to Chapter 5.

```sql
-- Sample SQL query for retrieving data
SELECT column1, column2
FROM table_name
WHERE condition;
```

## **2.6 The Relational Algebra**

The **relational algebra** encompasses operations on one or two relations, yielding a new relation as the result. Unary operations (e.g., select, project, rename) work on one relation, while binary operations (e.g., union, Cartesian product, set difference) operate on pairs of relations.

Though relational algebra forms the basis for SQL, database systems typically don't allow direct relational algebra queries. However, implementations exist for practicing relational algebra queries.

Relations contain unique tuples per mathematical definition, but duplicates are often permitted in database tables unless constrained. In formal relational algebra, duplicates are eliminated as per set theory.

### **2.6.1 The Select Operation**

Select operation chooses tuples satisfying a predicate denoted by the lowercase Greek letter sigma (σ). The predicate appears as a subscript, and the argument relation is in parentheses. For instance, to select Physics department instructors:
```
σ_{dept_name = “Physics”}(instructor)
```

Selection predicates can combine multiple conditions using logical connectives like and (∧), or (∨), and not (¬). Comparison operators (=, ≠, <, ≤, >, and ≥) are also valid.

### **2.6.2 The Project Operation**

Project operation (Π) returns a relation with specific attributes, eliminating duplicates. It's denoted by the uppercase Greek letter pi (Π), with desired attributes listed as a subscript. For example:
```
Π_{ID,name,salary}(instructor)
```

A generalized version allows expressions involving attributes in the list.

### **2.6.3 Composition of Relational Operations**

Relational operations can be composed into expressions. Resulting expressions maintain the relational type, allowing for seamless composition.
```
Π_{name}(σ_{dept_name = “Physics”}(instructor))
```

### **2.6.4 The Cartesian-Product Operation**

Cartesian product (×) combines information from two relations. Unlike mathematical Cartesian products, tuples are concatenated. Naming schema conventions are crucial for distinguishing attributes. For example, the result schema for `instructor × teaches`:
```
(instructor.ID, instructor.name, instructor.dept_name, instructor.salary, teaches.ID, course_id, sec_id, semester, year)
```

The resulting relation contains tuples generated from all possible pairs of tuples from the input relations, leading to a potentially large result set.

### 2.6.5**Join Operation**

To obtain information about instructors along with the course IDs of all courses they have taught, we utilize the join operation. While the Cartesian product of instructor and teaches combines data from both relations, it associates every instructor with every course, regardless of whether they taught it. By selecting tuples where instructor.ID = teaches.ID, we filter out irrelevant pairs. This results in instructors and their respective taught courses, eliminating those who didn't teach any course. Duplication of instructor IDs is resolved through projection to remove the teaches.ID column.

```sql
SELECT *
FROM instructor
JOIN teaches ON instructor.ID = teaches.ID;
```

### 2.6.6 **Set Operations**

Set operations like union (∪), intersection (∩), and set-difference (−) are employed to manipulate relations.

For instance, to find courses taught in Fall 2017 or Spring 2018, we perform selections on section relation based on semester and year. Then, the union of these sets gives the desired result, ensuring compatibility in terms of arity and attribute types.

```sql
(SELECT course_id FROM section WHERE semester = 'Fall' AND year = 2017)
UNION
(SELECT course_id FROM section WHERE semester = 'Spring' AND year = 2018);
```

To find courses taught in both Fall 2017 and Spring 2018, we perform set intersection on respective selections. Alternatively, set-difference identifies courses taught in Fall 2017 but not in Spring 2018.

```sql
(SELECT course_id FROM section WHERE semester = 'Fall' AND year = 2017)
INTERSECT
(SELECT course_id FROM section WHERE semester = 'Spring' AND year = 2018);

(SELECT course_id FROM section WHERE semester = 'Fall' AND year = 2017)
EXCEPT
(SELECT course_id FROM section WHERE semester = 'Spring' AND year = 2018);
```
**Relational Algebra Operations**

### 2.6.7 The Assignment Operation 
- **Functionality:** Assign parts of a relational-algebra expression to temporary relation variables.
- **Symbol:** Denoted by ←.
- **Example:** 
    ```
    courses_fall_2017 ← Π_{course_id} (σ_{semester = “Fall” ∧ year=2017}(section)) 
    courses_spring_2018 ← Π_{course_id} (σ_{semester = “Spring” ∧ year=2018}(section))
    courses_fall_2017 ∩ courses_spring_2018
    ```
- **Purpose:** Enables expressing complex queries as sequential programs.

### 2.6.8 The Rename Operation
- **Purpose:** Provides names to relational-algebra expressions.
- **Symbol:** Denoted by ρ (rho).
- **Usage:**
    - Assigns a name to a result: ρ (E) x.
    - Renames attributes: ρ_{x(A1, A2, ..., An)}(E).
- **Advantages:** Facilitates referencing the same relation multiple times in a query.
- **Example:** 
    ```
    Π ((σ (ρ (instructor) × σ (ρ (instructor))))) i.ID,i.name i.salary > w.salary i w.id=12121 w
    ```
- **Note:** Alternative positional notation exists but is less convenient for humans.

### 2.6.9 Equivalent Queries
- **Observation:** Multiple ways to express a query in relational algebra.
- **Example:** 
    - Query 1: σ_{dept_name = “Physics”}(instructor ⋈_{instructor.ID = teaches.ID} teaches)
    - Query 2: (σ_{dept_name = “Physics”}(instructor)) ⋈_{instructor.ID = teaches.ID} teaches
- **Equivalent Queries:** May have different sequences but yield the same result.
- **Optimization:** Database optimizers find efficient ways to compute results, not strictly following query sequence.

```sql
-- Example SQL query for equivalent queries
SELECT *
FROM instructor
JOIN teaches ON instructor.ID = teaches.ID
WHERE dept_name = 'Physics';
```

*Note: Relational algebra offers flexibility in query expression, allowing for optimization.*

# 3. **Introduction to SQL**

### 3.1 Overview
- **SQL:** Widely used database query language with functionalities beyond querying, including data structure definition, modification, and security constraints.
- **Purpose:** Present fundamental constructs and concepts of SQL; actual implementations may vary.

__SQL Language Evolution__
- **Origin:** Developed by IBM in the 1970s as Sequel, evolved into SQL (Structured Query Language).
- **Standardization:** ANSI and ISO published SQL standards: SQL-86, SQL-89, SQL-92, SQL:1999, SQL:2003, SQL:2006, SQL:2008, SQL:2011, SQL:2016.
- **Parts:** Data Definition Language (DDL), Data Manipulation Language (DML), Integrity, View Definition, Transaction Control, Embedded SQL, Dynamic SQL, Authorization.

__Chapter Contents__
- **Basic Features:** Survey of basic DML and DDL features since SQL-92.
- **Chapter 4:** Detailed coverage of SQL query language, including joins, views, transactions, integrity constraints, type system, and authorization.
- **Chapter 5:** Advanced features, such as accessing SQL from programming languages, functions, procedures, triggers, recursive queries, aggregation, and data analysis.

__Implementation Variations__
- **Differences:** SQL implementations may support nonstandard features and omit advanced or recent features.
- **Consultation:** Refer to user manuals for specific database systems to verify supported features.

*Note: Chapters 4 and 5 delve deeper into SQL query language and its advanced functionalities.*

# 3.2 **SQL Data Definition**

### 3.2.1 Basic Types
- **SQL DDL:** Defines relations in a database, including schema, attribute types, integrity constraints, indices, and storage structure.
- **Types:** char(n), varchar(n), int, smallint, numeric(p,d), real, double precision, float(n), nvarchar.
- **Null Value:** Represents an unknown or non-existent value; can be prohibited in certain cases.

### 3.2.2 Basic Schema Definition
- **Create Table Command:** Defines relation schema.
- **Attributes:** Name, type, optional constraints.
- **Primary Key:** Specifies unique non-null attributes.
- **Foreign Key:** References primary key attributes of another relation.
- **Not Null Constraint:** Prohibits null values for an attribute.

Integrity Constraints
- **Primary Key Constraint:** Ensures uniqueness and non-nullity.
- **Foreign Key Constraint:** Enforces referential integrity.
- **Not Null Constraint:** Excludes null values for an attribute.

Commands
- **Create Table:** Defines relation schema.
- **Drop Table:** Deletes relation and its schema.
- **Alter Table:** Adds or drops attributes from an existing relation.

```sql
-- Example: Create a department relation
CREATE TABLE department (
    dept_name VARCHAR(20),
    building VARCHAR(15),
    budget NUMERIC(12,2),
    PRIMARY KEY (dept_name)
);

-- Example: Add an attribute to an existing relation
ALTER TABLE department ADD location VARCHAR(50);

-- Example: Drop an attribute from an existing relation
ALTER TABLE department DROP building;
```

## 3.3 **Basic Structure of SQL Queries**

The basic structure of an SQL query comprises three clauses: **select**, **from**, and **where**. Queries operate on relations listed in the **from** clause, manipulate them as specified in the **where** and **select** clauses, and yield a relation as the output.

### 3.3.1 Queries on a Single Relation
- **Example 1:** Find the names of all instructors.
```sql
select name from instructor;
```
- **Example 2:** Find the department names of all instructors.
```sql
select dept_name from instructor;
```
- **Duplicate Handling:** SQL allows duplicates, but **distinct** keyword eliminates them.
```sql
select distinct dept_name from instructor;
```

__Arithmetic Expressions__
- The **select** clause can include arithmetic expressions.
```sql
select ID, name, dept_name, salary * 1.1 from instructor;
```

__The Where Clause__
- Filters rows based on specified predicates.
- Example: Find instructors in the Computer Science department with salary > $70,000.
```sql
select name from instructor where dept_name = 'Comp. Sci.' and salary > 70000;
```

### 3.3.2 Queries on Multiple Relations
- Combines information from multiple relations.
- Example: Retrieve instructor names, along with their department names and building names.
```sql
select name, instructor.dept_name, building from instructor, department where instructor.dept_name=department.dept_name;
```

__General SQL Query Form__
```sql
select A1, A2,...,An from r1, r2,...,rm where P;
```
- **A1, A2,...,An:** Attributes desired in the output.
- **r1, r2,...,rm:** Relations accessed.
- **P:** Predicate involving attributes in the **from** clause.

__Cartesian Product__
- Formed by relations listed in the **from** clause.
- Each tuple in one relation combines with every tuple in another.

__Understanding SQL Queries__
1. Generate Cartesian product of relations.
2. Apply predicates specified in the **where** clause.
3. Output attributes specified in the **select** clause.

*Note: Real SQL implementations optimize evaluation differently.*

**Remember:** Be cautious with predicates to avoid generating large Cartesian products.

## 3.4 **SQL Additional Basic Operations**

### 3.4.1 Rename Operation
- SQL supports renaming attributes in result relations using the `AS` clause.
- It allows changing attribute names and avoiding duplication.
- Syntax: `old-name AS new-name`.

Examples:
1. Renaming attributes in the result:
   ```sql
   SELECT name AS instructor_name, course_id
   FROM instructor, teaches
   WHERE instructor.ID = teaches.ID;
   ```

2. Renaming relations:
   ```sql
   SELECT T.name, S.course_id
   FROM instructor AS T, teaches AS S
   WHERE T.ID = S.ID;
   ```

### 3.4.2 String Operations
- SQL uses single quotes for string values.
- String functions include concatenation, substring extraction, case conversion, trimming, etc.
- Pattern matching is done using the `LIKE` operator with `%` and `_` wildcards.

Example:
- Finding departments with building names containing 'Watson':
  ```sql
  SELECT dept_name
  FROM department
  WHERE building LIKE '%Watson%';
  ```

### 3.4.3 Attribute Specification in Select Clause
- `*` symbol selects all attributes.
- `table_name.*` selects all attributes from a specific table.

Example:
- Selecting all attributes from the `instructor` table:
  ```sql
  SELECT instructor.*
  FROM instructor, teaches
  WHERE instructor.ID = teaches.ID;
  ```

### 3.4.4. Ordering the Display of Tuples
- `ORDER BY` clause sorts tuples in the result.
- Default order is ascending, but can be specified as descending.
- Supports sorting by multiple attributes.

Example:
- Listing instructors in Physics department alphabetically:
  ```sql
  SELECT name
  FROM instructor
  WHERE dept = 'Physics'
  ORDER BY name;
  ```

### 3.4.5 Where-Clause Predicates
- `BETWEEN` operator simplifies range queries.
- Allows specifying a range of values.

Example:
- Finding instructors with salary between $90,000 and $100,000:
  ```sql
  SELECT name
  FROM instructor
  WHERE salary BETWEEN 90000 AND 100000;
  ```

- Using row constructors for tuple comparison:
  ```sql
  SELECT name, course_id
  FROM instructor, teaches
  WHERE (instructor.ID, dept_name) = (teaches.ID, 'Biology');
  ```

## 3.5 **Set Operations in SQL**

### 3.5.1 Union Operation
- Query to find courses taught either in Fall 2017 or Spring 2018:
```sql
(select course_id from section where semester = 'Fall' and year = 2017)
union
(select course_id from section where semester = 'Spring' and year = 2018);
```
- Automatically eliminates duplicates from the result.

### 3.5.2 Intersect Operation
- Query to find courses taught in both Fall 2017 and Spring 2018:
```sql
(select course_id from section where semester = 'Fall' and year = 2017)
intersect
(select course_id from section where semester = 'Spring' and year = 2018);
```
- Automatically eliminates duplicates from the result.

### 3.5.3 Except Operation
- Query to find courses taught in Fall 2017 but not in Spring 2018:
```sql
(select course_id from section where semester = 'Fall' and year = 2017)
except
(select course_id from section where semester = 'Spring' and year = 2018);
```
- Outputs tuples from the first input that do not occur in the second input.

*Note: Parentheses around each select-from-where statement are optional but useful for readability.*

__Result Interpretation__
- Union: Automatically eliminates duplicates.
- Intersect: Automatically eliminates duplicates.
- Except: Outputs tuples not occurring in the second input.

*The number of duplicate tuples in the result depends on the number of duplicates in the input relations.*

## 3.6 **Null Values**

Null values pose challenges in relational operations, including arithmetic, comparison, and set operations.

- **Arithmetic Operations:** Result is null if any input value is null. For instance, "r.A + 5" yields null if "r.A" is null.

- **Comparison Operations:** Comparisons with nulls are problematic. SQL considers comparison with null as unknown, introducing a third logical value alongside true and false.

- **Boolean Operations:** SQL extends boolean operations to handle the unknown value:
  - "and": true and unknown is unknown, false and unknown is false, unknown and unknown is unknown.
  - "or": true or unknown is true, false or unknown is unknown, unknown or unknown is unknown.
  - "not": not unknown is unknown.

- **Where Clause Predicate:** If the predicate evaluates to false or unknown, the tuple is excluded from the result.

- **SQL Syntax:**
  - To find null values in "salary" column: `SELECT name FROM instructor WHERE salary IS NULL;`
  - To test if a comparison result is unknown: `SELECT name FROM instructor WHERE salary > 10000 IS UNKNOWN;`

- **Distinct Clause:** When comparing tuples for distinctness, SQL treats null values as identical. Thus, {('A',null), ('A',null)} are considered identical.

- **Set Operations:** Union, intersection, and except treat tuples as identical if they have the same values for all attributes, even if some values are null.

*Note: Null values introduce complexity in SQL operations and require careful handling to ensure accurate results.*

## 3.7 **Aggregate Functions in SQL**

Aggregate functions in SQL take a collection of values and return a single value. SQL offers five standard built-in aggregate functions:

- **Average:** `avg`
- **Minimum:** `min`
- **Maximum:** `max`
- **Total:** `sum`
- **Count:** `count`

The input to `sum` and `avg` must be a collection of numbers, while the other operators can work with non-numeric data types as well.

**Basic Aggregation**

For example, to find the average salary of instructors in the Computer Science department:

```sql
SELECT AVG(salary) AS avg_salary 
FROM instructor 
WHERE dept_name = 'Comp. Sci.';
```

Retaining duplicates is crucial for accurate aggregation. However, in cases where duplicates must be eliminated, the `distinct` keyword is used.

**Aggregation with Grouping**

The `group by` clause is utilized to apply aggregate functions to groups of tuples. For instance, to find the average salary in each department:

```sql
SELECT dept_name, AVG(salary) AS avg_salary 
FROM instructor 
GROUP BY dept_name;
```

The `having` clause is used to specify conditions on groups rather than individual tuples. For example, to find departments where the average salary exceeds $42,000:

```sql
SELECT dept_name, AVG(salary) AS avg_salary 
FROM instructor 
GROUP BY dept_name 
HAVING AVG(salary) > 42000;
```

**Aggregation with Null and Boolean Values**

Null values are handled according to specific rules. Aggregate functions treat nulls by ignoring them in their input collection. The `count (*)` function returns 0 for an empty collection, and other aggregate operations return null. Additionally, Boolean data types introduced in SQL:1999 allow for aggregation with `some` and `every` functions.

## 3.8 **Nested Subqueries**

SQL provides a mechanism for **nesting subqueries**, which are select-from-where expressions within another query. Subqueries are commonly used to perform tests for **set membership**, make set comparisons, and determine set cardinality. We explore various uses of nested subqueries in the where clause (Sections 3.8.1 to 3.8.4) and in the from clause (Section 3.8.5). Additionally, a class of subqueries called **scalar subqueries** is discussed in Section 3.8.7.

### 3.8.1 Set Membership 
- **in and not in operators**: Test for set membership or absence.
- Example: Finding courses taught in both Fall 2017 and Spring 2018 semesters using nested subqueries.

```sql
select distinct course_id
from section
where semester = 'Fall' and year = 2017 and
course_id in (select course_id from section
where semester = 'Spring' and year = 2018);
```

- **not in** construct: Used similarly to **in**, example: Finding courses taught in Fall 2017 but not in Spring 2018.

```sql
select distinct course_id
from section
where semester = 'Fall' and year = 2017 and course_id not in (select course_id
from section
where semester = 'Spring' and year = 2018);
```

- **Enumerated sets**: The operators can be used on enumerated sets as well.

```sql
select distinct name
from instructor
where name not in ('Mozart', 'Einstein');
```

### 3.8.2 Set Comparison
- **> some and > all comparisons**: Allow comparisons of sets.
- Example: Finding names of instructors whose salary is greater than at least one in the Biology department.

```sql
select name
from instructor
where salary > some (select salary
from instructor
where dept_name = 'Biology');
```

- **> all comparison**: Finds names of instructors with salary greater than all in the Biology department.

```sql
select name
from instructor
where salary > all (select salary
from instructor
where dept_name = 'Biology');
```

- **Other comparisons**: SQL also supports < some, <= some, >= some, = some, <> some, and similarly for **all**.


### **3.8.3 Test for Empty Relations**

SQL includes a feature for testing whether a subquery has any tuples in its result. The `exists` construct returns true if the argument subquery is nonempty. We can use it to find courses taught in both Fall 2017 and Spring 2018 semesters:

```sql
SELECT course_id
FROM section AS S
WHERE semester = 'Fall' AND year = 2017 AND
      EXISTS (SELECT *
              FROM section AS T
              WHERE semester = 'Spring' AND year = 2018 AND
                    S.course_id = T.course_id);
```

A subquery that uses a correlation name from an outer query is called a correlated subquery. Scoping rules apply for correlation names, allowing usage only within the subquery itself or its containing query.

We can test for the nonexistence of tuples in a subquery using the `not exists` construct. It can simulate set containment operations. For instance, to find students who have taken all Biology department courses:

```sql
SELECT S.ID, S.name
FROM student AS S
WHERE NOT EXISTS ((SELECT course_id
                   FROM course
                   WHERE dept_name = 'Biology')
                  EXCEPT
                  (SELECT T.course_id
                   FROM takes AS T
                   WHERE S.ID = T.ID));
```

### **3.8.4 Test for the Absence of Duplicate Tuples**

SQL includes the `unique` construct for testing duplicate tuples in a subquery. It returns true if the subquery contains no duplicates. To find courses offered at most once in 2017:

```sql
SELECT T.course_id
FROM course AS T
WHERE UNIQUE (SELECT R.course_id
              FROM section AS R
              WHERE T.course_id = R.course_id AND R.year = 2017);
```

`not unique` can be used to test for the existence of duplicate tuples. For instance, to find courses offered at least twice in 2017:

```sql
SELECT T.course_id
FROM course AS T
WHERE NOT UNIQUE (SELECT R.course_id
                  FROM section AS R
                  WHERE T.course_id = R.course_id AND R.year = 2017);
```

### **3.8.5 Subqueries in the From Clause**

SQL allows subquery expressions in the `from` clause. A select-from-where expression returns a relation, insertable into another select-from-where. For example, to find average instructors’ salaries of departments with average salary > $42,000:

```sql
SELECT dept_name
FROM (SELECT dept_name, AVG(salary) AS avg_salary
      FROM instructor
      GROUP BY dept_name) AS dept_avg
WHERE avg_salary > 42000;
```

Nested subqueries in the `from` clause are supported by most SQL implementations. The `lateral` keyword allows accessing attributes of preceding tables or subqueries in the same `from` clause. For example:

```sql
SELECT name, salary, avg_salary
FROM instructor AS I1, LATERAL (SELECT AVG(salary) AS avg_salary
                                 FROM instructor AS I2
                                 WHERE I2.dept_name = I1.dept_name);
```

### 3.8.6 **The With Clause**

The **WITH** clause in SQL allows the definition of temporary relations, accessible only within the query it's used in. It enhances query readability and logic, particularly useful for complex queries. Introduced in SQL:1999, it's supported by many, but not all, database systems.

Example:

```sql
WITH max_budget (value) AS (
    SELECT MAX(budget) FROM department
)
SELECT budget
FROM department, max_budget
WHERE department.budget = max_budget.value;
```

### 3.8.7 **Scalar Subqueries**

**Scalar subqueries** in SQL return a single value and can be used wherever an expression returning a value is permitted. They're commonly used in select, where, and having clauses. These subqueries may involve aggregates or not, and if they return more than one tuple at runtime, it results in an error.

Example:

```sql
SELECT dept_name, (SELECT COUNT(*) FROM instructor WHERE department.dept_name = instructor.dept_name) AS num_instructors
FROM department;
```

### 3.8.8 **Scalar Without a From Clause**

Certain queries necessitate calculation without reference to any relation or have subqueries without a from clause. In such cases, a special dummy relation like "dual" can be used to facilitate these queries.

Example:

```sql
SELECT (SELECT COUNT(*) FROM teaches) / (SELECT COUNT(*) FROM instructor) FROM dual;
```

Oracle provides a predefined relation called dual, containing a single tuple, for such purposes. To ensure precision, subquery results can be converted to floating point numbers before division.


# 3.9 **Modification of the Database**

### 3.9.1 Deletion
- **Delete Statement:** Removes tuples from a relation.
- Syntax: `delete from r where P;`
  - `r`: Relation name
  - `P`: Predicate
- Examples:
  - Delete instructors from the Finance department: `delete from instructor where dept_name = 'Finance';`
  - Delete instructors with salary between $13,000 and $15,000: `delete from instructor where salary between 13000 and 15000;`
  - Delete tuples associated with departments in the Watson building:
    ```sql
    delete from instructor
    where dept_name in (select dept_name from department where building = 'Watson');
    ```

### 3.9.2 Insertion
- **Insert Statement:** Adds tuples to a relation.
- Syntax: 
  - Single tuple: `insert into r values (val1, val2, ...);`
  - With attribute names: `insert into r(attr1, attr2, ...) values (val1, val2, ...);`
- Examples:
  - Insert a course: `insert into course values ('CS-437', 'Database Systems', 'Comp. Sci.', 4);`
  - Insert based on query result: 
    ```sql
    insert into instructor
    select ID, name, dept_name, 18000
    from student where dept_name='Music' and tot_cred>144;
    ```

### 3.9.3 Updates
- **Update Statement:** Modifies tuples in a relation.
- Syntax: `update r set attr = val where P;`
- Examples:
  - Increase all instructor salaries by 5%: `update instructor set salary= salary * 1.05;`
  - Increase salaries for instructors below $70,000: `update instructor set salary = salary * 1.05 where salary < 70000;`
  - Conditional updates:
    ```sql
    update instructor
    set salary = case
                when salary <= 100000 then salary * 1.05
                else salary * 1.03
                end;
    ```

SQL provides flexibility in data manipulation, allowing precise modifications to database content.

# 4. Intermediate SQL

## 4.1 **Join Expressions**

In Chapter 3, queries primarily used the Cartesian product operator to combine information from multiple relations, except when employing set operations. This section introduces "join" operations, enabling more natural query writing and expressing complex queries difficult with only Cartesian product.

All examples here involve two relations: **student** and **takes** (Figures 4.1 and 4.2). Note that **grade** attribute may have a null value for certain students indicating pending evaluation.

### 4.1.1 The Natural Join
- **SQL Query:** Computes courses each student has taken.
```sql
SELECT name, course_id
FROM student NATURAL JOIN takes
WHERE student.ID = takes.ID;
```
- Only outputs students who have taken courses.

- **Natural Join:** Operates on two relations, considering tuples with the same value on common attributes. For example, computing `student natural join takes` considers tuples where both have the same **ID** value.

- **Example Query Simplification:** 
```sql
SELECT name, course_id
FROM student NATURAL JOIN takes;
```

- **Result:** Relation with tuples containing student and course information.

- **Multiple Relations in FROM Clause:** 
```sql
SELECT A1, A2, ..., An
FROM r1 NATURAL JOIN r2 NATURAL JOIN ... NATURAL JOIN rm
WHERE P;
```

- **General FROM Clause Form:** 
```sql
FROM E1, E2, ..., En
```
Where each Ei can be a single relation or involve natural joins.

- **Query Example:**
```sql
SELECT name, title
FROM student NATURAL JOIN takes, course
WHERE takes.course_id = course.course_id;
```

### 4.1.2 Join Conditions
- **on Condition:** Allows specifying a general predicate over relations being joined, similar to a where clause predicate but using "on".

- **Query Example:**
```sql
SELECT *
FROM student JOIN takes ON student.ID = takes.ID;
```
Equivalent to: 
```sql
SELECT *
FROM student, takes
WHERE student.ID = takes.ID;
```

- **Join Expression with Alias:**
```sql
SELECT student.ID AS ID, name, dept_name, course_id, sec_id, semester, year, grade
FROM student JOIN takes ON student.ID = takes.ID;
```

- **Readability and Redundancy:** While on conditions may seem redundant, they enhance readability, especially for outer joins, and facilitate human understanding of SQL queries.

### 4.1.3 **Outer Joins**

Suppose we want to display a list of all students with their ID, name, dept name, and tot cred, along with the courses they have taken. Using `student natural join takes` may exclude students who haven't taken any courses. Outer join preserves such tuples by including null values.

Three forms of outer join:
- **Left outer join:** Preserves tuples from the left relation.
- **Right outer join:** Preserves tuples from the right relation.
- **Full outer join:** Preserves tuples from both relations.

**Left Outer Join:**
- Computes the inner join first.
- For unmatched tuples in the left relation, adds tuples with null values for attributes from the right relation.

Example query:
```sql
SELECT *
FROM student NATURAL LEFT OUTER JOIN takes;
```

**Right Outer Join:**
- Symmetric to left outer join.
- Adds tuples with null values from the left relation.

Example query:
```sql
SELECT *
FROM takes NATURAL RIGHT OUTER JOIN student;
```

**Full Outer Join:**
- Combines left and right outer join.
- Extends with nulls for unmatched tuples from both relations.

Example query:
```sql
SELECT *
FROM (SELECT *
      FROM student
      WHERE dept_name='Comp. Sci.')
NATURAL FULL OUTER JOIN (SELECT *
                         FROM takes
                         WHERE semester='Spring' AND year=2017);
```

**Join Types and Conditions**
- Normal joins are termed inner joins.
- `inner join` or `join` without the outer prefix defaults to inner join.
- `natural join` is equivalent to `natural inner join`.

Example queries:
```sql
SELECT *
FROM student JOIN takes USING (ID);

SELECT *
FROM student INNER JOIN takes USING (ID);
```

Various types of joins can be combined with any join condition (natural, using, or on).


# 4.2 **Views**

In databases, it's not always ideal for all users to access entire relations. Security and personalized access considerations may require limiting data visibility. For instance, a clerk may need to see certain instructor details but not salary.

- **Creating Views:** Views offer a solution by defining personalized collections of "virtual" relations that match user needs. These views are computed on-demand and not pre-stored.

    ```sql
    CREATE VIEW faculty AS SELECT ID, name, dept FROM instructor;
    ```

- **Using Views:** Once defined, views can be used in SQL queries like regular relations.

- **View Definition:** Views are created using the `CREATE VIEW` command, specifying a name and a query expression.

- **Materialized Views:** Some systems support storing views (materialized views) for faster access, updating them when underlying data changes. These views offer benefits but also incur storage and update overheads.

    ```sql
    CREATE MATERIALIZED VIEW departments_total_salary(dept_name, total_salary) AS
    SELECT dept_name, SUM(salary)
    FROM instructor
    GROUP BY dept_name;
    ```

- **Update of a View:** Updating views poses challenges as modifications must be translated into modifications of underlying relations. SQL defines conditions for views to be updatable, but updates may be rejected if they violate view conditions.
	- The from clause has only one database relation.
	- The select clause contains only attribute names of the relation and does not have any expressions, aggregates, or distinct specification.
	- Any attribute not listed in the select clause can be set to null; that is, it does not have a not null constraint and is not part of a primary key.
	- The query does not have a group by or having clause.

    ```sql
    CREATE VIEW history_instructors AS SELECT *
    FROM instructor
    WHERE dept_name = 'History'
    WITH CHECK OPTION;
    ```

- **Alternative Approaches:** Triggers offer an alternative for modifying databases through views, allowing custom actions for each case.

SQL:1999 introduces more complex rules for view updates, allowing updates through a larger class of views.

## 4.4 **Integrity Constraints**

Integrity constraints maintain **data consistency** in databases, preventing accidental data loss. They differ from security constraints, which control unauthorized access.

**Examples:**
- Instructor name cannot be null.
- Each instructor ID must be unique.
- Department names in the course relation must match those in the department relation.
- Department budgets must be greater than $0.00.

Constraints can be specified in the **create table** command or added later with **alter table**. They include:
- **not null**
- **unique**
- **check()**

**Not Null Constraint:**
Prohibits null values for attributes, ensuring meaningful data. For example:
```sql
name varchar(20) not null,
budget numeric(12,2) not null
```

**Unique Constraint:**
Ensures attribute uniqueness, unless explicitly declared as null. Attributes form a superkey.
```sql
unique (Aj1,Aj2,...,Ajm)
```

**Check Clause:**
Defines predicates to be satisfied by every tuple. Enables powerful type systems. For instance:
```sql
check (budget > 0)
```

**Referential Integrity:**
Ensures values in one relation match those in another. Foreign keys enforce these constraints.
- **Foreign key clause** specifies referencing attributes and referenced relation.
- Actions like **cascade** propagate changes across relations.
- Constraints can be deferred or deferrable, checked at transaction end.

**Naming Constraints:**
Constraints can be named for easier management.
```sql
constraint minsalary check (salary > 29000)
```
Later, constraints can be dropped by name.

**Complex Check Conditions and Assertions:**
SQL allows complex predicates and assertions, though not widely supported.
- Assertions express conditions to always satisfy.
- Assertions should be used judiciously due to overhead.

*SQL Queries:*
```sql
-- To add a named constraint
alter table instructor add constraint minsalary check (salary > 29000);

-- To drop a named constraint
alter table instructor drop constraint minsalary;
```

Complex check conditions and assertions provide powerful data integrity mechanisms but should be used cautiously due to potential overhead. They're implemented using triggers in some systems.

## 4.5 SQL Data Types and Schemas
This chapter extends the discussion from Chapter 3 on SQL data types and introduces user-defined types alongside built-in types.

### 4.5.1 Date and Time Types in SQL
- **Built-in Types**:
  - **date**: Stores a calendar date (year, month, day).
  - **time**: Stores time of day; `time(p)` variant includes fractional seconds and optional time-zone.
  - **timestamp**: Combines date and time; `timestamp(p)` variant allows fractional seconds and optional time-zone.

- **SQL Functions**:
  - **date 'YYYY-MM-DD'**: Sets a date.
  - **time 'HH:MM:SS'**: Sets a time.
  - **timestamp 'YYYY-MM-DD HH:MM:SS.FF'**: Sets a timestamp.
  - **extract(field from d)**: Extracts parts of date/time (e.g., year, month, day).
  - **current_date**, **current_time**, **localtime**, **current_timestamp**, **localtimestamp**: Functions to get current date and/or time.

### 4.5.2 Type Conversion and Formatting Functions
- **Type Conversion**:
  - **cast(e as t)**: Converts expression `e` to type `t`.
  - SQL example: `SELECT cast(ID as numeric(5)) as inst_id FROM instructor ORDER BY inst_id;` to convert and sort ID correctly.

- **Formatting Functions**:
  - **format**: Available in MySQL to format numbers.
  - **to_char**, **to_number**, **to_date**: Available in Oracle and PostgreSQL for data formatting.
  - **convert**: Used in SQL Server for data conversion.

- **Handling Null Values**:
  - **coalesce**: Returns the first non-null argument.
  - Example: `SELECT ID, coalesce(salary, 0) as salary FROM instructor;` shows salaries, substituting null with 0.
  - **decode**: Oracle-specific, allows replacing values based on a condition, e.g., replacing null with 'N/A'.
  - SQL example: `SELECT ID, decode(salary, null, 'N/A', salary) as salary FROM instructor;`

### 4.5.3 Default Values
- **Default Attributes in SQL Tables**:
  - SQL example: `CREATE TABLE student (ID varchar(5), name varchar(20) NOT NULL, dept_name varchar(20), tot_cred numeric(3,0) DEFAULT 0, PRIMARY KEY (ID));`
  - Illustrates setting a default value (0) for the `tot_cred` attribute. An `INSERT` statement can omit `tot_cred`, and it will default to 0.

### 4.5.4 Large-Object Types
- **Data Types for Large Objects**:
  - **clob**: Character Large Object, for storing large text data.
  - **blob**: Binary Large Object, for storing large binary data (e.g., images, videos).
  - SQL example: Declaring large object types, such as `book review clob(10KB)`, `image blob(10MB)`, `movie blob(2GB)`.

- **Handling Large Objects in SQL**:
  - Large objects are typically manipulated using locators, which are references to the data, allowing for efficient handling of very large data by fetching parts as needed, similar to file handling in operating systems.

### 4.5.5 User-Defined Types
- **SQL User-Defined Types**: SQL supports user-defined types, which include distinct types and structured data types.
  - **Distinct Types**: Used for defining simple types with unique domains. For example, monetary values in different currencies can be defined as distinct types to avoid programming errors during assignments or comparisons.
    ```sql
    CREATE TYPE Dollars AS NUMERIC(12,2) FINAL;
    CREATE TYPE Pounds AS NUMERIC(12,2) FINAL;
    ```
  - **Example Usage**:
    ```sql
    CREATE TABLE department (
      dept_name VARCHAR(20),
      building VARCHAR(15),
      budget Dollars
    );
    ```
  - **Type Conversion**: Requires explicit casting to convert between types and perform operations.
    ```sql
    CAST(department.budget AS NUMERIC(12,2))
    ```
  - **Structured Data Types**: Not covered in this section; discussed in Section 8.2, includes complex structures like nested records and arrays.

- **Domains vs. Types**:
  - **Domains**: Can have constraints (e.g., NOT NULL) and default values. Less strictly typed than user-defined types.
    ```sql
    CREATE DOMAIN DDollars AS NUMERIC(12,2) NOT NULL;
    ```
  - **Constraints**: Domains allow for specific constraints that must be met for the values.
    ```sql
    CREATE DOMAIN YearlySalary AS NUMERIC(8,2) CONSTRAINT salary_value_test CHECK (value >= 29000.00);
    ```

### 4.5.6 Generating Unique Key Values
- **Automatic Key Generation**: SQL supports auto-generating unique values for primary keys.
  - **Oracle/DB2 Syntax**:
    ```sql
    ID NUMBER(5) GENERATED ALWAYS AS IDENTITY;
    ```
  - **Inserting Data without Specifying ID**:
    ```sql
    INSERT INTO instructor (name, dept_name, salary) VALUES ('Newprof', 'Comp. Sci.', 100000);
    ```

### 4.5.7 Create Table Extensions
- **Create Table Like**:
  ```sql
  CREATE TABLE temp_instructor LIKE instructor;
  ```
- **Create Table As**:
  ```sql
  CREATE TABLE t1 AS (SELECT * FROM instructor WHERE dept_name = 'Music') WITH DATA;
  ```

### 4.5.8 Schemas, Catalogs, and Environments
- **Naming and Organization**:
  - **Schemas and Catalogs**: Provide a hierarchical structure for organizing database objects, preventing name clashes.
  - **Connection and Environment Setup**: Involves specifying a default catalog and schema that uniquely identifies database relations.
  - **SQL Environment**: Includes user identifiers and operates within the context of a schema.

- **Schema and Catalog Management**:
  - **Creating/Dropping Schemas**:
    ```sql
    CREATE SCHEMA univ_schema;
    DROP SCHEMA univ_schema;
    ```
  - **Catalogs**: Creation and management of catalogs vary across different SQL implementations and are not standardized.

This summary captures the essential concepts and SQL codes from the sections on user-defined types, unique key value generation, table creation extensions, and the organization of schemas, catalogs, and SQL environments.

## 4.6 Index Definition in SQL
- **Purpose of Indexes**: Enhance the efficiency of queries that access only a small fraction of records, avoiding the need to scan all records.
- **Index Usage**: Allows quick retrieval of tuples with specific attribute values, such as department names or IDs in a relation.
- **Physical vs. Logical Schema**: Indices are part of the physical schema and are used to improve transaction processing and integrity constraint enforcement, though they are not essential for correctness.
- **Control Over Indices**:
  - SQL provides control over index creation and removal through data-definition-language commands.
  - Indices can be on a single attribute or a list of attributes.
- **SQL Commands for Indices**:
  - Create Index: `CREATE INDEX <index-name> ON <relation-name> (<attribute-list>);`
  - Unique Index: `CREATE UNIQUE INDEX <index-name> ON <relation-name> (<attribute-list>);` marks the search key as a candidate key.
  - Drop Index: `DROP INDEX <index-name>;`
  - Indices can be B-tree, hash, or clustered, details of which are studied further in databases.
- **Creating an Index**:
  ```sql
  CREATE INDEX <index-name> ON <relation-name> (<attribute-list>);
  ```
  Example:
  ```sql
  CREATE INDEX deptindex ON instructor (dept_name);
  ```

- **Unique Index Creation**:
  ```sql
  CREATE UNIQUE INDEX <index-name> ON <relation-name> (<attribute-list>);
  ```
  Example:
  ```sql
  CREATE UNIQUE INDEX deptindex ON instructor (dept_name);
  ```

- **Dropping an Index**:
  ```sql
  DROP INDEX <index-name>;
  ```


## 4.7 Authorization
- **Types of Privileges**:
  - **Read**: Authorization to read data.
  - **Insert**: Authorization to insert new data.
  - **Update**: Authorization to update data.
  - **Delete**: Authorization to delete data.
  - Privileges can be granted on specific parts of the database like relations or views.

- **Authorization Process**:
  - SQL checks if a user's query or update is authorized based on granted privileges.
  - Unauthorized queries or updates are rejected.

- **Additional Authorizations**:
  - Users may have schema-level authorizations (e.g., create, modify, or drop relations).
  - Privileges can be passed on (granted) or withdrawn (revoked) by users who have them.

- **Database Administrator**:
  - Holds the highest level of authority, similar to a superuser in an OS, capable of authorizing users and restructuring the database.

### 4.7.1 Granting and Revoking of Privileges
- **SQL Privileges**:
  - Includes `select`, `insert`, `update`, `delete`, and `all privileges`.
  - `grant` statement assigns privileges; `revoke` removes them.

```sql
grant <privilege list> on <relation name or view name> to <user/role list>;
revoke <privilege list> on <relation name or view name> from <user/role list>;
```

- **Example of Granting Privileges**:
  - `grant select on department to Amit, Satoshi;`
  - Grants select privilege on the department relation to users Amit and Satoshi.

- **Revoking Privileges**:
  - `revoke select on department from Amit, Satoshi;`
  - Removes select privilege from users Amit and Satoshi.

### 4.7.2 Roles
- **Role-Based Authorization**:
  - Roles group authorizations for ease of management (e.g., instructor, dean).
  - Users are granted roles which simplify assigning and managing permissions.

```sql
create role instructor;
grant select on takes to instructor;
```

- **Role Inheritance**:
  - Roles can inherit privileges from other roles.
  - E.g., a dean may inherit privileges from the instructor and teaching assistant roles.

### 4.7.3 Authorization on Views
- **Views for Restricted Access**:
  - Users can be granted access to specific data through views without giving them access to entire relations.

```sql
create view geo_instructor as (select * from instructor where dept_name = 'Geology');
```

- **Authorization Checks on Views**:
  - When a query involves a view, the system checks if the user has the necessary privileges on the underlying data.

### 4.7.4 Authorizations on Schema
- **Schema Modifications**:
  - Only the schema owner can modify it unless specific privileges like `references` are granted.

```sql
grant references (dept_name) on department to Mariano;
```

### 4.7.5 Transfer of Privileges
- **With Grant Option**:
  - Allows users to pass on the privileges they have been granted to others.

```sql
grant select on department to Amit with grant option;
```

- **Revocation and its Impact**:
  - Revoking a privilege can have a cascading effect, impacting users who were indirectly granted the privilege.

### 4.7.6 Revoking of Privileges
- **Cascading Revocation**:
  - Default behavior in SQL; can be controlled with `restrict` or `cascade` options in the `revoke` statement.

### 4.7.7 Row-Level Authorization
- **Fine-Grained Access Control**:
  - Some systems support authorization at the row level, allowing for precise control over who can see or manipulate individual rows.

Overall, SQL provides a robust framework for managing database authorizations at various levels, including the ability to assign and revoke privileges and the use of roles to simplify and secure access management.

# 5. Advanced SQL

## 5.1 Accessing SQL from a Programming Language
- **SQL and Programming Languages**: SQL's declarative nature is simpler for queries but lacks the expressive power and functionality for nondeclarative tasks found in languages like C, Java, or Python. These include generating reports, user interaction, and handling GUI output, which are essential for integrated applications.

- **Approaches to SQL Access**:
  - **Dynamic SQL**: Enables SQL query construction at runtime via general-purpose programming languages using functions or methods. This allows submission and retrieval of query results dynamically.
  - **Embedded SQL**: Embeds SQL in a host language, with SQL statements processed at compile-time into function calls. This method interacts with databases at runtime via an API providing dynamic SQL capabilities.

- **Challenges**: Mixing SQL with general-purpose languages presents difficulties due to different data handling methods. SQL operates on relational data, returning sets, whereas programming languages operate on individual variables.

Subsection Details:
- **JDBC (Java Database Connectivity)**:
  - **Connection Establishment**: Utilizes `getConnection()` from `java.sql.DriverManager` to establish connections using database URLs, user IDs, and passwords.
  - **Executing SQL Statements**: SQL commands are sent to the database for execution via the `Statement` class. Methods like `executeQuery()` and `executeUpdate()` handle SQL queries and updates respectively.
  - **Handling Results**: Results are managed via `ResultSet` objects, with data fetched using methods like `getString()` and `getFloat()`.
  - **Prepared Statements**: Enhances security and efficiency by using placeholders for values in SQL commands, preventing SQL injection risks.
  - **Exception Handling and Resource Management**: Utilizes try-with-resources for safe management of database connections and statements to avoid resource leaks.

- **Metadata Handling**:
  - **ResultSetMetaData**: Provides metadata about the result set of a query, such as column names and types.
  - **DatabaseMetaData**: Offers detailed information about the database system, including supported features and schema details.

- **Advanced JDBC Features**:
  - **Callable Statements**: Supports SQL stored procedures and functions.
  - **Transaction Management**: Controls transaction commitment and rollback with `setAutoCommit()`, `commit()`, and `rollback()`.
  - **Large Object Handling**: Methods like `getBlob()` and `setBlob()` manage large data objects efficiently, using streams.

- **Security Considerations**:
  - **Prepared Statements**: Crucial for preventing SQL injection, ensuring that user inputs are safely incorporated into SQL commands.
  - **SQL Injection Risks**: Demonstrates the dangers of constructing SQL queries directly from user inputs and the importance of using prepared statements.

SQL Code Examples:
- **Connecting to a Database**:
  ```sql
  getConnection("jdbc:oracle:thin:@db.yale.edu:2000:univdb", "user", "password");
  ```

- **Executing an Update**:
  ```sql
  stmt.executeUpdate("INSERT INTO instructor VALUES (...)");
  ```

- **Fetching Query Results**:
  ```sql
  ResultSet rset = stmt.executeQuery("SELECT * FROM instructor");
  ```

- **Prepared Statement for Insert**:
  ```sql
  PreparedStatement prepStmt = conn.prepareStatement("INSERT INTO instructor VALUES (?, ?, ?, ?)");
  prepStmt.setString(1, "88878");
  prepStmt.setString(2, "Perry");
  prepStmt.setString(3, "Finance");
  prepStmt.setFloat(4, 125000);
  prepStmt.executeUpdate();
  ```

### 5.1.2 Database Access from Python
- **Database Operations in Python**:
  - **Insert Queries**: Use placeholders ("%s") to parameterize SQL queries, similar to JDBC prepared statements.
  - **Transaction Management**: Updates must be manually committed using the `commit()` method.
  - **Error Handling**: Utilizes `try`, `except` blocks to catch and print exceptions.
  - **Result Iteration**: A `for` loop is used to traverse and access query results.
  - **Database Drivers**: Examples include `psycopg2` for PostgreSQL, `MySQLdb` for MySQL, and `cx_Oracle` for Oracle. The `pyodbc` driver supports ODBC connections.
  - **API Differences**: Minor variations exist in the Python Database API across different drivers, particularly in connection parameters.

### 5.1.3 ODBC (Open Database Connectivity)
- **ODBC API**: Allows applications to connect to any ODBC-supported database server for querying and updates.
- **ODBC Usage**:
  - **Connection Setup**: Involves allocating SQL environment and database connection handles, using `SQLConnect`.
  - **Query Execution**: Uses `SQLExecDirect` to send SQL commands.
  - **Result Binding**: `SQLBindCol` binds C variables to SQL query results.
  - **Data Fetching**: `SQLFetch` retrieves query results into bound C variables.
  - **Transaction Control**: `SQLSetConnectOption` to disable auto-commit, requiring explicit commit or rollback.
  - **ODBC Conformance Levels**: Vary from core features to more advanced features involving arrays and detailed catalog information.

### 5.1.4 Embedded SQL
- **Embedded SQL in Host Languages**: SQL can be embedded into programming languages like C, Java, Cobol, etc.
- **Preprocessing and Compilation**:
  - **Preprocessor Role**: Translates embedded SQL into host language code before compilation.
  - **Runtime Execution**: Unlike JDBC, embedded SQL is preprocessed, which can catch SQL-related errors early.
- **Cursor Usage**: Cursors manage row-by-row processing of query results.
- **Embedded SQL Syntax**: Uses `EXEC SQL` to denote embedded SQL statements; host language variables within SQL statements are prefixed with a colon (":").
- **Disadvantages of Embedded SQL**:
  - **Debugging Complexity**: Generated host language code complicates debugging.
  - **Syntax Clashes**: Potential conflicts with updates in host language syntax.
- **Alternatives to Embedded SQL**: Most systems now use dynamic SQL due to its flexibility; Microsoft's LINQ is an exception, integrating query capabilities into the host language.

```sql
-- Example of an SQL statement with parameters
INSERT INTO department VALUES(?, ?, ?);
```

```sql
-- Turning off auto-commit on a connection
SQLSetConnectOption(conn, SQL_AUTOCOMMIT, 0);

-- Explicitly committing a transaction
SQLTransact(conn, SQL_COMMIT);
```

## 5.2 Functions and Procedures
- **Purpose**: Allows developers to write and store their own functions and procedures in the database for invocation from SQL statements. Useful for specialized data types (e.g., images, geometric objects).
- **Business Logic Storage**: Enables encapsulating business rules as database-stored procedures, enhancing maintainability and accessibility.
- **Implementation Variability**: Although based on the SQL standard, most databases implement proprietary versions (e.g., PL/SQL for Oracle, TransactSQL for Microsoft SQL Server, PL/pgSQL for PostgreSQL).

### 5.2.1 Declaring and Invoking SQL Functions and Procedures
- **Function Example**: Function to count instructors in a department, usable in queries to fetch department names and budgets with more than 12 instructors.

    ```sql
    select dept_name, budget
    from department
    where dept_count(dept_name) > 12
    ```

- **Performance Considerations**: Potential performance issues when invoking complex user-defined functions on large datasets.
- **Table Functions**: Functions that return tables, acting like parameterized views.

    ```sql
    select *
    from table(instructor_of('Finance'));
    ```

- **Procedures Example**: Procedures can handle input (`in`) and output (`out`) parameters, invoked using SQL or embedded SQL.

    ```sql
    create procedure dept_count_proc(in dept_name varchar(20), out d_count integer)
    begin
      select count(*) into d_count from instructor
      where instructor.dept_name = dept_count_proc.dept_name
    end
    declare d_count integer;
    call dept_count_proc('Physics', d_count);
    ```

### 5.2.2 Language Constructs for Procedures and Functions
- **SQL as a Programming Language**: Supports variables, assignments, compound statements, loops, and conditional statements to enable complex procedural logic within SQL.
- **Transaction Control**: The `begin atomic ... end` statement ensures all contained statements are executed as a single transaction.
- **Exception Handling**: SQL can signal and handle exceptions, supporting robust error management within procedural code.

    ```sql
    declare out_of_classroom_seats condition
    declare exit handler for out_of_classroom_seats
    begin
      -- sequence of statements
    end
    ```

### 5.2.3 External Language Routines
- **Integration with External Languages**: SQL functions/procedures can be defined in languages like Java, C#, C, or C++ for enhanced efficiency and capability.
- **Security and Performance Considerations**: While external routines can be more performant, they may introduce security risks or system instability. Safe execution environments like sandboxes can mitigate some risks.

    ```sql
    create procedure dept_count_proc(in dept_name varchar(20), out count integer)
    language C
    external name '/usr/avi/bin/dept_count_proc';
    ```

- **Support Across Databases**: Different databases support various external languages, impacting the portability and maintenance of database applications.

This summary encapsulates the key aspects of SQL functions and procedures as discussed, highlighting their practical applications, performance considerations, and integration with external programming languages.

## 5.3 Triggers
- **Definition**: A statement executed automatically by the system due to a database modification.
- **Configuration**:
  - **Event**: Specifies when the trigger is checked.
  - **Condition**: Must be met for the trigger execution to proceed.
  - **Action**: Defined operations that execute when the trigger fires.

### 5.3.1 Need for Triggers
- **Purpose**:
  - Enforce integrity constraints not possible through standard SQL constraints.
  - Automate tasks and alerts based on specific database changes.
- **Examples**:
  - **Course Credits**: Automatically update a student's total credits when they enroll in a new course.
  - **Inventory Management**: Auto-generate reorder entries when inventory falls below a minimum level.

### 5.3.2 Triggers in SQL
- **Syntax Variability**: Different SQL systems may use non-standard syntax, but core concepts remain similar.
- **Referential Integrity**:
  - **Inserts**: Triggers ensure inserted values are valid.
  - **Updates/Deletes**: Triggers manage changes to maintain data integrity.
- **SQL Syntax for Trigger**:
  ```sql
  CREATE TRIGGER example_trigger AFTER UPDATE OF grade ON takes
  REFERENCING NEW ROW AS nrow
  WHEN (nrow.grade IS NOT NULL AND nrow.grade <> 'F')
  BEGIN
      UPDATE students SET tot_cred = tot_cred + nrow.credits
      WHERE student_id = nrow.student_id;
  END;
  ```

### 5.3.3 When Not to Use Triggers
- **Alternatives**:
  - Foreign-key constraints with cascade actions.
  - Materialized views for fast data access, maintained by the database system.
  - Database replication facilities for data redundancy and backup.
- **Challenges**:
  - Triggers can complicate understanding and maintenance of database constraints.
  - Improper use can lead to infinite trigger loops or unintended actions during data backup operations.

**Considerations**:
- Triggers are powerful for automatic and immediate response to data changes but should be used judiciously, considering potential complexity and alternative database features.

## 5.4 Recursive Queries
- **Context**: Discussion on how to find both direct and indirect prerequisites for a course (e.g., CS-347) at a university.
- **Scenario**: Courses like CS-319, CS-315, and CS-101 indirectly act as prerequisites for CS-347 through a series of prerequisite chains.
- **Transitive Closure**: Describes the relationship where a course is a direct or indirect prerequisite of another course. This concept applies to multiple hierarchies such as organizational structures or mechanical parts.

### 5.4.1 Transitive Closure Using Iteration
- **Method**: Utilizes iterative queries to find all courses that are prerequisites using three temporary tables (`c_prereq`, `new_c_prereq`, `temp`) to track and update the list of prerequisites.
- **Process**:
  - Insert direct prerequisites into `new_c_prereq`.
  - Move these courses to `c_prereq`.
  - Find new prerequisites, store in `temp`, and update `new_c_prereq`.
  - Continue until no new courses are added, indicating all indirect prerequisites are found.
- **SQL Features**: Use of `create temporary table` and handling potential cycles with the `except` clause to ensure accurate results despite unusual data structures like cycles.

### 5.4.2 Recursion in SQL
- **Preferred Method**: Recursive view definitions simplify expressing transitive closures, preferred over iterative methods for clarity and conciseness.
- **SQL Syntax**:
  - Use `WITH RECURSIVE` to define recursive views.
  - Combine a base (non-recursive) and a recursive query.
  - Achieve a fixed point where no new tuples are added to define the complete set of direct and indirect prerequisites.
- **Example Query**: To find all prerequisites for a course like CS-347, including direct and indirect ones.
  
```sql
WITH RECURSIVE rec_prereq AS (
  SELECT prereq.course_id, prereq.prerequisite
  FROM prereq
  WHERE course_id = 'CS-347'  -- Base case: Direct prerequisites
  UNION
  SELECT p.course_id, r.prerequisite
  FROM prereq p
  JOIN rec_prereq r ON p.prerequisite = r.course_id  -- Recursive step: Indirect prerequisites
)
SELECT * FROM rec_prereq;
```
- **Constraints**: Recursive queries in SQL must be monotonic; they cannot include aggregation, NOT EXISTS, or EXCEPT operations on the recursive view.

Implementation Notes
- **Monotonic Constraint**: Ensures that the recursive query results are predictable and expand as more tuples are added to the view.
- **Alternative Syntax**: Some SQL systems like Oracle use different syntax (e.g., `START WITH` / `CONNECT BY PRIOR`) for hierarchical queries.
- **Applicability**: Beyond academic course prerequisites, recursive queries are useful in organizational charts, parts inventories, and more, demonstrating wide applicability in various domains.

## 5.5 Advanced Aggregation Features in SQL

### 5.5.1 Ranking
- **Purpose**: To determine the position of a value within a set, such as assigning ranks to students based on GPA.
- **SQL Query for Ranking**: Uses `ORDER BY` to sort the data before ranking.
  ```sql
  SELECT ID, rank() OVER (ORDER BY GPA DESC) AS s_rank FROM student;
  ```
- **Handling Ties**: The `rank()` function assigns the same rank to tied values but skips subsequent ranks (e.g., two students tied for rank 1 will cause the next rank to be 3).
- **Dense Ranking**: `dense_rank()` avoids gaps in ranking sequence, treating ties differently by not skipping ranks after ties.
- **Handling Nulls**: Ranking can treat nulls as either the highest or lowest values, specified using `NULLS FIRST` or `NULLS LAST`.
  ```sql
  SELECT ID, rank() OVER (ORDER BY GPA DESC NULLS LAST) AS s_rank FROM student_grades;
  ```
- **Efficiency Concerns**: Direct SQL ranking can be more efficient than manual computation, which could be quadratic in performance for large datasets.
- **Partitioned Ranking**: Allows ranking within subsets of data, such as by department.
  ```sql
  SELECT ID, dept_name, rank() OVER (PARTITION BY dept_name ORDER BY GPA DESC) AS dept_rank FROM dept_grades ORDER BY dept_name, dept_rank;
  ```

### 5.5.2 Windowing
- **Purpose**: To compute aggregates over specific ranges or "windows" of data, which can be based on a range of tuples or specific values.
- **Example Usage**: Analyzing trends by computing moving averages over time.
- **SQL Query for Fixed Range Window**:
  ```sql
  SELECT year, AVG(num_credits) OVER (ORDER BY year ROWS 3 PRECEDING) AS avg_total_credits FROM tot_credits;
  ```
- **SQL Query for All Previous Years**:
  ```sql
  SELECT year, AVG(num_credits) OVER (ORDER BY year ROWS UNBOUNDED PRECEDING) AS avg_total_credits FROM tot_credits;
  ```

### 5.5.3 Pivoting
- **Purpose**: To transform rows into columns, typically used in data analysis to view data from different perspectives.
- **SQL Query for Pivot**:
  ```sql
  SELECT * FROM sales PIVOT (SUM(quantity) FOR color IN ('dark', 'pastel', 'white'));
  ```
- **Application**: Useful for summarizing sales data by different attributes like item name, color, and size in a compact form.

### 5.5.4 Rollup and Cube
- **Purpose**: To perform multiple `GROUP BY` queries in a single SQL query, useful for generating comprehensive summaries across various dimensions.
- **Rollup Example**:
  ```sql
  SELECT item_name, color, SUM(quantity) FROM sales GROUP BY ROLLUP(item_name, color);
  ```
- **Cube Example**:
  ```sql
  SELECT item_name, color, clothes_size, SUM(quantity) FROM sales GROUP BY CUBE(item_name, color, clothes_size);
  ```
- **Grouping Sets**: Provides the ability to specify exact groupings.
  ```sql
  SELECT item_name, color, clothes_size, SUM(quantity) FROM sales GROUP BY GROUPING SETS((color, clothes_size), (clothes_size, item_name));
  ```
- **Handling Nulls with Grouping Functions**: Distinguishes between nulls generated by rollup/cube operations and actual data nulls.
  ```sql
  SELECT (CASE WHEN grouping(item_name) = 1 THEN 'all' ELSE item_name END) AS item_name, (CASE WHEN grouping(color) = 1 THEN 'all' ELSE color END) AS color, SUM(quantity) AS quantity FROM sales GROUP BY ROLLUP(item_name, color);
  ```

These features enhance SQL's capability to handle complex data aggregation and analysis tasks efficiently and effectively.

# 6. Database Design Using the E-R Model

### Lecture Summary: Overview of the Database Design Process

## 6.1 Overview of the Design Process
- **Complexity**: Involves designing database schema, access/update programs, and a security scheme.
- **User-Centric**: Designing process primarily driven by user needs.

### 6.1.1 Design Phases
- **Initial Phase**:
  - **User Interaction**: Essential for characterizing data needs through extensive interaction with domain experts and users.
  - **Outcome**: Specification of user requirements, typically captured textually.
- **Conceptual Design**:
  - **Data Model Selection**: Choosing a data model to translate requirements into a conceptual schema.
  - **Entity-Relationship Model**: Commonly used to represent the conceptual schema through entities, attributes, relationships, and constraints.
  - **Entity-Relationship Diagram**: Provides a graphical representation of the schema.
  - **Schema Review**: Ensures all data requirements are met and checks for redundancies.
  - **Functional Requirements**: Schema should support specified operations like modifying, searching, and deleting data.
- **Logical Design**:
  - **Schema Mapping**: Translates high-level conceptual schema into a relational schema suitable for implementation.
  - **Implementation Data Model**: Typically the relational model.
- **Physical Design**:
  - **Database Implementation**: Specifies physical features like file organization and indexing.
  - **Schema Flexibility**: Physical schema is more adaptable post-implementation compared to logical schema.

### 6.1.2 Design Alternatives
- **Entity Representation**:
  - **Entities**: Distinct items such as people, places, and products.
  - **Examples**: In a university database, entities might include instructors, students, departments, courses, and sections of courses.
- **Avoiding Design Pitfalls**:
  - **Redundancy**: Avoid repeating information across the database to prevent inconsistencies (e.g., course titles stored with each offering).
    ```sql
    -- Example to avoid redundancy by normalizing data
    CREATE TABLE Courses (
      CourseID int PRIMARY KEY,
      Title varchar(100),
      DeptName varchar(100),
      Credits int
    );

    CREATE TABLE CourseOfferings (
      OfferingID int PRIMARY KEY,
      CourseID int,
      Semester varchar(10),
      Year int,
      FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
    );
    ```
  - **Incompleteness**: Ensure all necessary aspects of the enterprise can be modeled, avoiding schemas that cannot represent all required information.
- **Modeling Relationships**:
  - **Consideration**: Whether a relationship (like a sale) is an interaction between entities or an entity itself.

## 6.2 The Entity-Relationship Model
- **Purpose**: Facilitates database design through an enterprise schema representing the logical structure of a database.
- **Utility**: Maps real-world interactions onto a conceptual schema, widely used in database design tools.
- **Key Concepts**:
  - **Entity Sets**: Groups of entities (real-world objects) sharing properties. Examples include people in a university categorized as 'instructors' or 'students'.
  - **Relationship Sets**: Associations among entities, such as the advisor relationship between instructors and students.
  - **Attributes**: Properties of entities, such as a person’s ID or name.

- **E-R Diagrams**: Visual representation of databases using entity sets (rectangles) and relationship sets (diamonds).

### 6.2.1 Entity Sets
![[Pasted image 20240413154133.png|400]]
- **Definition**: An entity is an object distinct from other objects, identified by a unique set of properties (e.g., a person identified by a person ID).
- **Types of Entities**: Can be concrete (like a book) or abstract (like a course offering).
- **Attributes**: Descriptive properties unique to each entity within a set. Common attributes include ID, name, and department name. Key attributes are underlined in diagrams.

### 6.2.2 Relationship Sets
![[Pasted image 20240413154151.png|500]]
- **Definition**: Associations among multiple entities, such as an instructor advising a student.
- **Complex Relationships**: In addition to binary relationships (involving two entity sets), relationships can be ternary (involving three entity sets) or even more complex.
- **Attributes of Relationships**: Relationships can have descriptive attributes (like grades in a student-section relationship).

![[Pasted image 20240413154258.png|500]]
- **E-R Diagram Representation**:
  - Entities are shown as rectangles divided into two sections for the entity name and its attributes.
  - Relationships are depicted with diamonds, linked to entities with lines. Attributes of relationships are shown with dashed lines connecting to the diamonds.

![[Pasted image 20240413154217.png|400]]
- **Role of Entities in Relationships**: Entities may participate in multiple roles within relationships. For example, a course might be related to another as a prerequisite.

SQL Representation (Hypothetical Queries)
```sql
-- Assuming the existence of tables for entity sets and relationships:
-- Query to find the advisor for a specific student:
SELECT instructor.name
FROM advisor
JOIN instructor ON advisor.instructor_id = instructor.id
JOIN student ON advisor.student_id = student.id
WHERE student.name = 'Shankar';

-- Query to list all courses and their prerequisites:
SELECT course.title AS course, prereq.title AS prerequisite
FROM course
JOIN prereq ON course.prereq_id = prereq.course_id;
```

## 6.3 Complex Attributes
![[Pasted image 20240413154541.png|500]]
- **Domain**: Each attribute has a set of allowed values known as its domain. For instance, the domain for `course_id` might include all text strings of a specified length, whereas the domain for `semester` might be the strings {Fall, Winter, Spring, Summer}.

- **Attribute Types in the E-R Model**:
  - **Simple and Composite Attributes**:
    - **Simple Attributes**: These are not divided into smaller parts. 
    - **Composite Attributes**: These can be broken down into smaller subparts or attributes. For example, an `address` attribute might be a composite of street, city, state, and postal code, allowing for a more structured data approach.
    - **Hierarchical Composite Attributes**: A composite attribute like `street` could further be divided into street number, street_name, and apartment number, forming a hierarchical structure.
  - **Single-valued and Multivalued Attributes**:
    - **Single-valued Attributes**: Attributes that have only one value for each entity, like a `student ID`.
    - **Multivalued Attributes**: Attributes that can have multiple values for a single entity. For instance, an instructor might have multiple phone numbers or several dependents, represented as `{phone number}` or dependent names respectively.
  - **Derived Attributes**: Attributes whose values are calculated from other attributes. An example is `students_advised`, where the number of students an instructor advises can be counted from associated student entities.

- **Null Values in Attributes**:
  - **Indications of Null Values**:
    - **Not Applicable**: The attribute value does not exist for the entity.
    - **Unknown**: The attribute value is missing (exists but not known) or it is not known whether the value exists.
  - **Examples**: A null value for `middle initial` might indicate a non-applicable situation (e.g., the person has no middle name). A null in `apartment number` could imply the absence of an apartment in the address or unknown information about the apartment.
![[Pasted image 20240413154637.png|500]]
Representation in E-R Notation:
- **Composite Attributes**: Illustrated as components within a larger attribute, such as an `address` consisting of street number, street name, and apartment number.
- **Multivalued Attributes**: Denoted by curly braces around the attribute, e.g., `{phone number}`.
- **Derived Attributes**: Represented with parentheses, e.g., `age ()`.

SQL Representation:
- **Handling Multivalued Attributes**: In SQL, these might be handled by creating separate tables to store the multiple values due to the relational model's constraints.
- **Derived Attributes**: Can be managed through SQL queries that calculate values based on other data in the database.

```sql
-- Example SQL query to derive 'students_advised' attribute
SELECT instructor_id, COUNT(student_id) AS students_advised
FROM advising_relationships
GROUP BY instructor_id;
```


## 6.4 Mapping Cardinalities
- **Mapping Cardinalities or Cardinality Ratios**: Express the number of entities in one entity set that can be associated with entities in another entity set via a relationship set. Primarily used in binary relationships but applicable to more complex sets.

![[Pasted image 20240413154906.png|500]]
- **Types of Cardinalities in Binary Relationship Sets**:
  - **One-to-one**: Each entity in entity set A is associated with at most one entity in entity set B and vice versa.
  - **One-to-many**: One entity in A can be associated with multiple entities in B, but each entity in B can only be associated with one entity in A.
  - **Many-to-one**: One entity in B can be associated with multiple entities in A, but each entity in A can only be associated with one entity in B.
  - **Many-to-many**: Entities in A can be associated with any number of entities in B and vice versa.

- **Real-world Implications**:
  - Used to model real-world relationships such as advising relationships at universities.
  - Depending on university policies, an advising relationship could be one-to-many (one instructor advises many students) or many-to-many (students advised by multiple instructors).

- **Representation in E-R Diagrams**:
  - **Cardinality Representation**: Indicated with directed lines (arrows) for one-to-one or one-to-many relationships, and undirected lines for many-to-one or many-to-many relationships.
  - **Participation**: Total participation is shown with double lines, indicating that every entity in the set participates in at least one relationship.
  - **Cardinality Constraints**: Often noted on the lines connecting entities, with notation like 1..1 (exactly one), 0..* (zero or more).

- **Examples**:
  - **Advisor Relationship Set**:
    - Total participation of students (every student must have an advisor).
    - Partial participation of instructors (not all instructors must advise).

![[Pasted image 20240413154944.png|500]]
- **Complex Constraints**:
  - Allows specifying minimum and maximum numbers of participations of entities in relationships.
  - E-R diagrams can alternatively show these constraints with lines and arrows instead of cardinality limits.

- **SQL Representation**:
  - Specific cardinality constraints can influence SQL schema design, affecting keys and foreign key constraints, but detailed SQL code generation from cardinality specifications isn't directly applicable without the broader context of the database schema design.

## 6.5 Primary Key

- **Purpose**: Distinct identification of entities within an entity set and relationships within a relationship set based on their attribute values.

### 6.5.1 Entity Sets
- **Uniqueness**: Each entity must have attribute values that uniquely identify it, ensuring no two entities in an entity set have the same values for all attributes.
- **Key Types**:
  - **Superkey**: A set of attributes that can uniquely identify entities.
  - **Candidate Key**: A minimal superkey; minimal set of attributes needed to uniquely identify entities.
  - **Primary Key**: A candidate key selected to uniquely identify entities in a database table.

### 6.5.2 Relationship Sets
- **Identification of Relationships**: Using the primary keys of the participating entity sets to form a unique primary key for the relationship set.
- **Composition of Primary Key**:
  - If **no attributes** are associated with a relationship set \( R \), then the primary key is the union of the primary keys from all participating entity sets \(\text{primary-key}(E1) \cup \text{primary-key}(E2) \cup \ldots \cup \text{primary-key}(En)\).
  - If **attributes are associated** \( a1, a2, \ldots, am \) with the relationship set \( R \), the primary key includes these attributes alongside the primary keys from the entity sets.
- **Handling Non-Unique Attribute Names**: Attributes are renamed to include the entity set name to maintain uniqueness.
- **Special Cases**:
  - **Many-to-Many Relationships**: The primary key is the union of the primary keys of the involved entities.
  - **Many-to-One and One-to-Many Relationships**: The primary key of the "many" side is used.
  - **One-to-One Relationships**: The primary key of either entity can be used.
  - **Nonbinary Relationships**: The primary key depends on cardinality constraints; if constraints are complex, a combination of primary keys from multiple entities may form the candidate key.

### 6.5.3 Weak Entity Sets
![[Pasted image 20240413155256.png|500]]
- **Definition**: Entities that do not have enough attributes to form a primary key on their own and are dependent on another entity set, termed as an identifying entity set.
- **Identification**: Weak entities use the primary key of the identifying entity set combined with discriminator attributes to form a unique identifier.
- **Total Participation**: Every weak entity must be associated with an identifying entity, indicating a many-to-one relationship from the weak entity to the identifying entity.
- **ER Diagram Representation**: Weak entity sets are depicted with a double rectangle and connected to their identifying entity set with a double diamond.

SQL Representation of Primary Key Constraints:
For example, defining primary keys within an SQL database for an entity set and a relationship set could be represented as:
```sql
-- Creating an entity table with a primary key
CREATE TABLE Entity (
    EntityID INT NOT NULL,
    Attribute1 VARCHAR(255),
    Attribute2 VARCHAR(255),
    PRIMARY KEY (EntityID)
);

-- Creating a relationship table with a composite primary key
CREATE TABLE Relationship (
    Entity1ID INT NOT NULL,
    Entity2ID INT NOT NULL,
    PRIMARY KEY (Entity1ID, Entity2ID),
    FOREIGN KEY (Entity1ID) REFERENCES Entity(EntityID),
    FOREIGN KEY (Entity2ID) REFERENCES Entity(EntityID)
);
```
This SQL code defines primary keys for a hypothetical entity and its relationship set, ensuring uniqueness and referential integrity in a relational database system.


## 6.6 Removing Redundant Attributes in Entity Sets

When constructing a database using the E-R model, identifying relevant entity sets and attributes is crucial. In the context of a university organization, key entity sets such as **student** and **instructor** were determined. Attributes for each entity set need careful selection to avoid redundancy and accurately reflect the organization's structure.

__Entity and Attribute Selection__
- **Instructor Entity Set**: Attributes include ID, name, salary, and dept_name.
- **Department Entity Set**: Contains dept_name, building, and budget. Dept_name is the primary key.

__Identifying Redundancies__
Redundant attributes across entity sets can complicate the database schema and should be minimized:
- **Dept_name**: Redundant in the **instructor** entity set since it's already defined as a primary key in the **department** entity set. Such redundancy is avoided by establishing relationships rather than duplicating attributes.
- **Time Slot ID and Building/Room Number**: Similar redundancies were identified in the **section** entity set, which contains attributes that are primary keys in the **time slot** and **classroom** entity sets, respectively.

__Relationship Sets__
Properly defining relationship sets helps eliminate unnecessary attributes within entity sets by using relationships:
- **inst_dept**: Connects instructors with their departments.
- **stud_dept**: Associates students with departments.
- **teaches**, **takes**, **sec_class**, **sec_time_slot**, **advisor**, **prereq**: Additional relationships defining interactions between courses, sections, students, and instructors.

__E-R Design Validation__
The final E-R design was validated to ensure no entity set contains attributes made redundant by relationship sets. The design replaces redundant attributes with relationship sets, capturing all necessary information while maintaining simplicity and integrity.
![[Pasted image 20240413160105.png]]
__Diagram and Constraints__
- **E-R Diagram**: Reflects the university structure with constraints like total participation of instructors in departments, indicated by a double line between the **instructor** and **inst_dept**.
- **Unique Constraints**: Arrows from relationship sets to departments indicate that each entity (instructor, course, student) is associated with exactly one department.

__SQL Considerations__
In relational databases derived from E-R diagrams, SQL is used to manage and query data. For instance, removing an instructor's department could be represented in SQL as follows:

```sql
ALTER TABLE Instructor
DROP COLUMN dept_name;
```

This change in the database schema reflects the design principle of minimizing redundancy by managing relationships rather than duplicating data across tables.