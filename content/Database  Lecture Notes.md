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
	