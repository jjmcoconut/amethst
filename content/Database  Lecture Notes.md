

## 4.2 Views
- **Purpose of Views**: Not all users need to see all data. Views help restrict access to specific parts of the database for security and data organization tailored to user needs.

### 4.2.1 View Definition
- **SQL Command for Creating Views**:
  ```sql
  create view v as <query expression>;
  ```
  - **Example for Restricting Data** (hiding salary data from clerks):
    ```sql
    create view faculty as select ID, name, dept from instructor;
    ```
  - **Example for Course Information** (listing Physics courses in Fall 2017):
    ```sql
    create view physics_fall_2017 as
    select course.course_id, sec_id, building, room_number
    from course, section
    where course.course_id = section.course_id
    and course.dept_name = 'Physics'
    and section.semester = 'Fall'
    and section.year = 2017;
    ```

### 4.2.2 Using Views in SQL Queries
- **Usage Example**:
  - Finding Physics courses in a specific building:
    ```sql
    select course_id
    from physics_fall_2017
    where building = 'Watson';
    ```
  - Views behave like regular tables in queries but are computed on demand.

### 4.2.3 Materialized Views
- **Definition**: Stored views that are updated when underlying data changes, enhancing query performance but requiring maintenance.
- **Maintenance**:
  - Immediate update or lazy update upon access.
  - Systems may allow periodic updates; contents may be stale if not updated frequently.

### 4.2.4 Update of a View
- **Challenges in Modifying Views**:
  - Not all views are updatable due to the complexity of reflecting changes in the underlying tables.
  - Example problematic update:
    ```sql
    insert into faculty values ('30765', 'Green', 'Music');
    ```
    - Requires a default or null salary which may not be acceptable.

- **Conditions for Updatable Views**:
  - Single table in the `FROM` clause.
  - Only attribute names in the `SELECT` clause, no aggregates or expressions.
  - Attributes not listed can be null.

- **Example of Restricted Update**:
  - View where only history department instructors are shown:
    ```sql
    create view history_instructors as select *
    from instructor
    where dept_name = 'History';
    ```
  - Problems with inserting tuples that do not match the view's filter condition.

- **SQL Standards for View Updates**:
  - SQL:1999 specifies more complex rules for view updates.
  - Use of `WITH CHECK OPTION` to ensure inserted or updated rows satisfy the view's filter.

## 4.3 Transactions

- A transaction consists of a sequence of query and/or update statements and is a unit of work
- The SQL standard specifies that a transaction begins implicitly when an SQL statement is executed
- The transaction must end with one of the following statements
	- Commit: the updates performed by the transaction become permanent in the database 
	- Rollback: all the updates performed by the SQL statements in the transaction are undone
- Thus, the atomicity of a transaction is guaranteed 
	- Either fully executed or rolled back as if it never occurred


## 4.4 **Integrity Constraints**

- **Purpose**: Ensure database consistency by guarding against accidental data corruption, contrasting with security constraints which prevent unauthorized access.
- **Examples**:
  - Instructor names cannot be null.
  - Unique instructor IDs.
  - Department names in courses must match those in the department relation.
  - Department budgets must exceed $0.00.

- **Specification**: Typically specified during schema design and included in SQL `CREATE TABLE` commands or added later via `ALTER TABLE`.

### 4.4.1 Constraints on a Single Relation
- **Primary SQL Commands**: `CREATE TABLE` which may include constraints like `NOT NULL`, `UNIQUE`, and `CHECK(<predicate>)`.

### 4.4.2 Not Null Constraint
**Purpose**: Prevent null values in critical fields, ensuring data completeness.
- **SQL Example**:
  ```sql
  CREATE TABLE student (
      name VARCHAR(20) NOT NULL,
      budget NUMERIC(12, 2) NOT NULL
  );
  ```
- **Use Case**: Null values are prohibited in primary keys to maintain entity integrity.

### 4.4.3 Unique Constraint
**Definition**: Ensures no two tuples have the same values in specified attributes.
- **SQL Syntax**:
  ```sql
  UNIQUE (attribute1, attribute2, ...)
  ```
- **Details**: Attributes under `UNIQUE` constraint can still be null unless explicitly declared as `NOT NULL`.

### 4.4.4 The Check Clause
**Purpose**: Enforces that attributes satisfy specified conditions, acting as a dynamic assertion within the database.
- **SQL Example**:
  ```sql
  CREATE TABLE department (
      budget NUMERIC(12, 2),
      CHECK (budget > 0)
  );
  CREATE TABLE section (
      semester VARCHAR(6),
      CHECK (semester IN ('Fall', 'Winter', 'Spring', 'Summer'))
  );
  ```
- **Special Cases**: Null values do not violate `CHECK` constraints unless explicitly stated by a `NOT NULL` constraint.
- **Limitations**: Current SQL standards do not support subqueries within `CHECK` predicates.


### 4.4.5 Referential Integrity
**Referential Integrity Constraints**: Ensure a value in one relation (referencing relation) also appears in another (referenced relation), typically implemented using foreign keys.
  - **Foreign Key Example**: In a university database, the `course` table references the `department` table to ensure all listed departments exist.

 
**SQL Foreign Key Declaration**: Specified within the `CREATE TABLE` statement using the `FOREIGN KEY` clause.
  ```sql
  CREATE TABLE course (
    dept_name VARCHAR(20),
    FOREIGN KEY (dept_name) REFERENCES department(dept_name)
  );
  ```

**Referential Actions**: SQL allows specifying actions like `ON DELETE CASCADE` and `ON UPDATE CASCADE` to handle changes that might violate integrity constraints.
  ```sql
  CREATE TABLE course (
    ...
    dept_name VARCHAR(20),
    FOREIGN KEY (dept_name) REFERENCES department ON DELETE CASCADE ON UPDATE CASCADE,
    ...
  );
  ```

**Handling Null Values**: SQL allows foreign keys to contain null values unless specified as `NOT NULL`. Null foreign keys automatically satisfy integrity constraints.

### 4.4.6 Assigning Names to Constraints
- **Naming Constraints**: Enhances manageability by allowing specific constraints to be named and later dropped if necessary.
  ```sql
  ALTER TABLE instructor DROP CONSTRAINT minsalary;
  ```

### 4.4.7 Integrity Constraint Violation During a Transaction
**Deferred Constraint Checking**: SQL supports deferring integrity checks to the end of a transaction, allowing intermediate states that might otherwise violate constraints.
  - **Example Scenario**: Inserting related data across tables (e.g., spouses in a `person` table) that temporarily violates foreign key constraints until all inserts are complete.

### 4.4.8Complex Check Conditions and Assertions
**Advanced Integrity Constraints**: SQL standards allow specifying complex conditions using subqueries and assertions, though not widely supported.
  - **Assertion Example**: Ensuring total credits in the `student` table match sum of completed course credits.
  ```sql
  CREATE ASSERTION credits_earned CHECK (
    NOT EXISTS (
      SELECT ID FROM student
      WHERE tot_cred <> (
        SELECT COALESCE(SUM(credits), 0)
        FROM takes NATURAL JOIN course
        WHERE student.ID = takes.ID AND grade IS NOT NULL AND grade <> 'F'
      )
    )
  );
  ```
- **Use of Assertions**: Provides a powerful but costly method to enforce data integrity. Care is advised due to potential performance impact. Assertions are not typically supported by common database systems, but similar functionality can be achieved using triggers.


## 5.1 Accessing SQL from a Programming Language
SQL, while powerful and declarative for querying, lacks the full capabilities of general-purpose languages, necessitating integration with such languages for comprehensive application development. Here are the key reasons and methods for combining SQL with general-purpose languages:

**Reasons for Integration**:
  1. **Expressiveness Limitations**: Some complex queries require the advanced capabilities of languages like C, Java, or Python, which are not available in SQL.
  2. **Nondeclarative Actions**: Tasks such as outputting reports, user interaction, or integrating query results into user interfaces must be handled outside SQL.

**Methods of Accessing SQL**:
  1. **Dynamic SQL**:
     - Enables runtime construction and execution of SQL queries within general-purpose programs.
     - Supported by procedural and object-oriented languages through functions or methods that allow queries to be built as character strings, executed, and their results retrieved into program variables.
     - **Standards and APIs**:
       - **JDBC**: Java API that facilitates database connection and operations.
       - **ODBC**: Initially for C, now supports C++, C#, Ruby, Go, PHP, and Visual Basic.
       - **Python Database API**: Connects Python programs to databases.
       - **ADO.NET**: For .NET languages (e.g., C# and Visual Basic), allows data access similar to JDBC but also supports non-relational data sources.

  2. **Embedded SQL**:
     - Incorporates SQL directly within the code, identified during the compilation.
     - Uses a preprocessor to convert SQL into function calls that interact with the database at runtime through an API providing Dynamic SQL capabilities.
     - Specific to the database being used and recognized at compile time, contrasting with the runtime flexibility of Dynamic SQL.

**Challenges**:
  - **Data Manipulation Mismatch**: SQL operates on relational data and returns sets (relations), while general-purpose languages work on individual variables. Bridging this gap requires mechanisms to adapt set-oriented SQL results into the variable-oriented structure of programming languages.

**Alternative Approaches**:
  - **Embedded Databases**: Discussed as another option for integrating databases within applications, offering localized data management without server connectivity.

#### Code Example: SQL Queries

```sql
-- Example of a Dynamic SQL query in a programming language (Pseudocode)
query = "SELECT * FROM users WHERE age > 21";
result = execute_query(query);
while (has_more_results(result)) {
    user = fetch_next(result);
    print(user.name);
}
```

### 5.3.2 Triggers in SQL
**Purpose and Usage**: Triggers in SQL are used to ensure data integrity and automate data management tasks by responding to specific changes or events within a database.
**Standard vs. Non-standard Syntax**: While the SQL standard defines a specific syntax for triggers, most databases implement variations of this syntax, making it crucial to understand the concepts broadly applicable across different systems.

**Referential Integrity Example**:
  - **Insert Trigger**: Ensures that `time slot id` in the `section` relation is valid upon insertions. The trigger checks each new row and rolls back the transaction if it violates referential integrity.
  - **SQL Query**:
    ```sql
    -- This example code checks the validity of time slot IDs during insertion
    create trigger check_time_slot_id after insert on section
    referencing new row as nrow
    for each row
    when (nrow.time_slot_id is not valid)
    begin atomic
      rollback transaction;
    end;
    ```
  - **Delete Trigger**: Ensures that a `time slot id` being deleted is not referenced in the `section` relation, maintaining referential integrity.

**Handling Updates and Deletes**:
  - Triggers must also manage updates and deletes to both the `section` and `time slot` tables to ensure ongoing referential integrity.

**Update Specific Attributes**:
  - Triggers can be configured to respond only to changes in specific attributes, which prevents unnecessary executions and enhances performance.
  - **SQL Query**:
    ```sql
    create trigger update_credits after update of takes on grade
    referencing new row as nrow
    referencing old row as orow
    for each row
    when nrow.grade <> 'F' and nrow.grade is not null and (orow.grade = 'F' or orow.grade is null)
    begin atomic
      update student set tot_cred = tot_cred + (select credits from course where course.course_id = nrow.course_id where student.id = nrow.id);
    end;
    ```

**Trigger Options**:
  - **Before and After**: Triggers can be set to activate before or after an event, allowing them to either prevent or correct errors.
  - **Row vs. Statement Level**: Triggers can operate on individual rows or on all rows affected by a SQL statement, with different implications for performance and complexity.
  - **Enabling and Disabling**: Triggers can be dynamically enabled or disabled, allowing for flexible database management.

**Advanced Uses and Customization**:
  - **Set Value Modification**: Triggers can modify data as it is being inserted or updated, such as changing blank values to null.
  - **SQL Query**:
    ```sql
    create trigger set_null before update of takes on grade
    referencing new row as nrow
    for each row
    when (nrow.grade = ' ')
    begin atomic
      set nrow.grade = null;
    end;
    ```


### 5.3.3 When Not to Use Triggers
Triggers are powerful tools in database management, but there are instances where their use is not advisable or necessary. Alternative solutions often offer more efficient or clearer implementations.

**Alternative to Triggers**: 
  - **Foreign-Key Constraints**: Using triggers to mimic the 'on delete cascade' feature is more complex than using the built-in cascade feature of foreign-key constraints, making the database harder to understand.
  - **Materialized Views**: While triggers can maintain materialized views, such as updating a count of students per course section, modern databases support automatic maintenance of materialized views, negating the need for manual trigger management.
    - **SQL Example**: 
      ```sql
      CREATE TABLE section_registration (
          course_id VARCHAR(20), 
          sec_id VARCHAR(10), 
          semester VARCHAR(10), 
          year INT, 
          total_students INT
      );

      SELECT course_id, sec_id, semester, year, COUNT(ID) AS total_students 
      FROM takes 
      GROUP BY course_id, sec_id, semester, year;
      ```

**Database Replication**: Triggers were historically used to maintain replicas of databases by recording changes in delta relations. Modern systems, however, offer built-in replication facilities that are more efficient and robust than trigger-based solutions.

**Triggers in Backup and Replication Scenarios**: 
  - **Unintended Execution**: Triggers may execute unintended actions during data loads from backups or when updates at a primary site are replicated at a backup site. To manage this, triggers can be disabled or set as 'not for replication' to prevent execution in replication scenarios.
  - **System Variables**: Some systems use a variable to indicate a database is a replica, allowing trigger bodies to exit without executing if this condition is true.

**Care in Trigger Use**:
  - **Runtime Errors**: Errors within triggers can cause the transaction that activated the trigger to fail.
  - **Chain Reactions**: Improperly designed triggers can initiate a chain of triggers, potentially leading to infinite loops. Database systems may limit the number of permissible trigger cascades to prevent such issues.

**Alternatives to Triggers**:
  - **Stored Procedures**: Many tasks assigned to triggers can be more appropriately handled by stored procedures, which offer more direct control and can be easier to manage.


### 5.4.2 Recursion in SQL
**Recursion in SQL**: Utilized to specify transitive closure more conveniently than iteration, allowing for recursive view definitions.
**Example Use Case**: Defining courses that are prerequisites (both directly and indirectly) for a specific course such as CS-347.

**SQL Standard on Recursion**:
  - Supports a limited form of recursion using the `with recursive` clause.
  - Recursive views are temporary and defined in terms of themselves.

**Recursive View Definition**:
  - Must be the union of a **base query** (nonrecursive) and a **recursive query**.
  - The process continues iteratively until no new tuples are added to the view, reaching a **fixed point** where the view contains the tuples in the fixed-point instance.

**Query Example**:
  - To find all prerequisites of CS-347, modify the query with a `where` clause filtering by the course ID.

- **SQL Query Syntax for Recursive Operation**:
```sql
with recursive rec_prereq(course_id, prereq_id) as (
    select course_id, prereq_id from prereq
    union
    select rec_prereq.course_id, prereq.prereq_id
    from rec_prereq, prereq
    where rec_prereq.prereq_id = prereq.course_id
)
select * from rec_prereq;
```
  - This recursive SQL query efficiently finds all direct and indirect prerequisites for a course.

**Restrictions on Recursive Queries**:
  - Must be **monotonic**, meaning the result must grow as more tuples are added to the view relation.
  - Cannot use operations like aggregation on the recursive view, `not exists` with a subquery involving the recursive view, or set difference (`except`) where the right-hand side uses the recursive view.

**Other SQL Implementations**:
  - Some databases like Oracle use different syntax such as `start with / connect by prior` for hierarchical queries.

## 5.5 Advanced Aggregation Features in SQL

### 5.5.1 Ranking
**Purpose**: Ranking helps determine the position of a value within a set, such as ranking students by GPA.
  
**SQL Constructs for Ranking**:
  - Standard SQL ranking is challenging and may combine SQL with other programming languages for efficiency.
  - Example ranking query:
    ```sql
    select ID, rank() over (order by GPA desc) as s_rank
    from student_grades;
    ```
  - An additional `order by` is required to sort by rank:
    ```sql
    select ID, rank() over (order by GPA desc) as s_rank
    from student_grades
    order by s_rank;
    ```

**Handling Ties**:
  - The `rank` function assigns the same rank to tied values, creating gaps in subsequent rankings.
  - The `dense_rank` function does not create gaps after ties, providing a sequential ranking.

**Null Values**:
  - Nulls can be treated as the highest values or controlled with `nulls first` or `nulls last` options:
    ```sql
    select ID, rank() over (order by GPA desc nulls last) as s_rank
    from student_grades;
    ```
  - Traditional SQL approach to simulate rank:
    ```sql
    select ID, (1 + (select count(*) from student_grades B where B.GPA > A.GPA)) as s_rank
    from student_grades A
    order by s_rank;
    ```

**Partitioned Ranking**:
  - Ranking within categories (e.g., by department) uses the `partition by` clause:
    ```sql
    select ID, rank() over (partition by dept_name order by GPA desc) as dept_rank
    from dept_grades
    order by dept_name, dept_rank;
    ```

**Efficient Ranking**:
  - Nested queries for top-n results:
    ```sql
    select *
    from (select ID, rank() over (order by GPA desc) as s_rank from student_grades)
    where s_rank <= 5;
    ```
  - This may return more than `n` results due to ties.

**Alternative Ranking Functions**:
  - **Percent Rank**: Calculates rank as a fraction of the total count.
  - **Cume Dist**: Cumulative distribution function.
  - **Row Number**: Assigns a unique number to each row based on order.
  - **Ntile**: Divides data into nearly equal buckets, useful for histograms:
    ```sql
    select ID, ntile(4) over (order by GPA desc) as quartile
    from student_grades;
    ```
  - These functions offer various ways to interpret and analyze data rankings differently depending on the specific requirements of the analysis.

This comprehensive exploration of SQL ranking functions underscores their versatility and power in data analysis, allowing for detailed and nuanced insights into data sets.

### 5.5.2 Windowing
**Window Queries**: Compute aggregate functions over ranges of tuples, useful for analyzing trends over time. Windows may overlap, allowing tuples to contribute to multiple windows, unlike partitions where a tuple contributes to only one.

**Use Cases**:
  - **Trend Analysis**: Analyzing sales data to understand trends affected by external factors like weather. Similarly, stock market trends can be analyzed using various moving averages.

**SQL Windowing Feature**:
  - Simplifies queries that compute aggregates over sliding windows of data.
  - Example: Calculating moving averages over fixed periods without writing cumbersome SQL for each window.

**SQL Queries for Windowing**:
  - **Fixed Window Size Example**:
    ```sql
    SELECT year, AVG(num_credits) OVER (ORDER BY year ROWS 3 PRECEDING) AS avg_total_credits
    FROM tot_credits;
    ```
    This query calculates the average number of credits over the three preceding years.

  - **Unbounded Preceding Window Example**:
    ```sql
    SELECT year, AVG(num_credits) OVER (ORDER BY year ROWS UNBOUNDED PRECEDING) AS avg_total_credits
    FROM tot_credits;
    ```
    This computes the average over all prior years to a given year.

  - **Variable Size Window Example**:
    ```sql
    SELECT year, AVG(num_credits) OVER (ORDER BY year ROWS BETWEEN 3 PRECEDING AND 2 FOLLOWING) AS avg_total_credits
    FROM tot_credits;
    ```
    Averages credits over a window that starts three years before and ends two years after the current year.

  - **Department-Specific Window Example**:
    ```sql
    SELECT dept_name, year, AVG(num_credits) OVER (PARTITION BY dept_name ORDER BY year ROWS BETWEEN 3 PRECEDING AND CURRENT ROW) AS avg_total_credits
    FROM tot_credits_dept;
    ```
    This query partitions data by department and computes the average credits for the department over a defined window.

**Range vs. Rows**:
  - `ROWS`: Specifies the window in terms of physical rows.
  - `RANGE`: Covers all tuples with a particular value rather than a specific number of tuples.
  - Note: The `RANGE` keyword might not be fully implemented in all SQL systems.







**Database**
- Organized collection of interrelated data  
    that models some aspect of the real-world
- Core component of most computer applications

- For example, let’s build a database that models a K-POP digital music store to keep track of artists and albums
- We need to store:  
    Information about Artists  
    What Albums those Artists related

CSV File Strawman
Storing our database as comma-separated value (CSV) files that we manage ourselves in our application code
- A CSV file is created for each entity (i.e., table)
- The application must parse the files each time they want to read/update records
- e.g., create two csv files for artists and albums respectively

Problems with CSV Files?
- Integrity
	- How do we ensure that the artist is the same for each album entry?
		- e.g., BTS, Bangtan Boys, 방탄소년단
	- What if somebody overwrites the album year with an invalid string?
	- What if there are multiple artists on an album? 
	- What happens if we delete an artist that has albums?
- Implementation
	- How do you find a particular record?
	- What if we now want to create a new application that uses the same database?
	- What if two threads try to write to the same file at the same time?
- Durability
	- What if the machine crashes while our program is updating a record?
	- What if we want to replicate the database on multiple machines for high availability?

**Database Systems**
- DBMS contains information about a particular enterprise
	- Collection of interrelated data
	- Set of programs to access the data 
	- An environment that is both convenient and efficient to use
- Database systems are used to manage collections of data that are:
	- Highly valuable
	- Relatively large
	- Accessed by multiple users and applications, often at the same time
- A modern database system is a complex software system whose task is to manage a large, complex collection of data
- Databases touch all aspects of our lives

Database Applications Examples
- Enterprise information
    - Sales: customers, products, purchases
    - Accounting: payments, receipts, assets
    - Human resources: information about employees, salaries, payroll taxes
- Manufacturing: management of production, inventory, orders, supply chain
- Banking and finance
    - Customer information, accounts, loans, banking transactions
    - Credit card transactions
    - Finance: sales and purchases of financial instruments (e.g., stocks and bonds); storing real-time
        market data
- Universities: registration, grades
	Airlines: reservations, schedules
	- Telecommunication: records of calls, texts, and data usage, generating monthly
	bills, maintaining balances on prepaid calling cards
	- Web-based services
		- Online retailers: order tracking, customized recommendations
		- Online advertisements
	- Document databases: encyclopedia, blogs
	- Navigation systems: maintaining the locations of various places of interest along with the exact routes of roads, train systems, buses, etc.
	- LLM applications: document embedding vectors

Purpose of Database Systems
In the early days, database applications were built directly on top of file systems, which leads to:
- Data redundancy and inconsistency
	- Data is stored in multiple file formats resulting in duplication of information in different files
- Difficulty in accessing data
	- A new program needs to be implemented to carry out each new task
- Data isolation
	- Due to multiple files and formats, writing a program to retrieve the appropriate data is difficult
- Integrity problems
	- Integrity constraints (e.g., account balance > 0) become “buried” in program code rather than
	being stated explicitly
		- Hard to add new constraints or change existing ones
- Atomicity of updates
	- Failures may leave database in an inconsistent state with partial updates carried out
		- e.g., Transfer of funds from one account to another should either complete or not happen at all
- Concurrent access by multiple users
	- Concurrent access is needed for high performance
	- Uncontrolled concurrent accesses can lead to inconsistencies
		- e.g., Two people reading a balance (say 100) and updating it by withdrawing money (say 50 each) at the same time
- Security problems
	- It is hard to provide user access to some, but not all, data
	