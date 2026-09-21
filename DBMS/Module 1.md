```
                    DATABASE SYSTEM
                          │
        ┌─────────────────┼─────────────────┐
        ↓                 ↓                 ↓
      DBMS              Users          Database Languages
        │
        ↓
   Abstraction
        │
        ↓
   Architecture
        │
        ↓
 Relational Model
        │
        ↓
 Constraints + Keys
        │
        ↓
   ER Model
        │
        ↓
 ER Design → Mapping → Relational Tables
```

# 1. Concept of DBMS

## What is a Database?

A **database** is an organized collection of related data that can be stored, accessed, managed, and updated efficiently.

For example, a college might maintain:

STUDENT
────────────────────────────
Student_ID   Name     Branch
101          Rahul            CSE
102          Priya             ECE
103          Amit             CSE

This is data organized in a meaningful way.

## What is a DBMS?

**DBMS = Database Management System**

A DBMS is software that allows users and applications to:

- Create databases
- Retrieve data
- Modify or update data
- Delete data
- Store data
- Control access to data
- Maintain consistency
- Recover data after failures

Examples:

- MySQL
- PostgreSQL
- Oracle Database
- Microsoft SQL Server
- MongoDB

However, MongoDB is a **NoSQL DBMS**, whereas MySQL, PostgreSQL, Oracle, etc. are primarily **relational DBMSs (RDBMSs)**.

Without DBMS some problems may arise:
### Problem 1 — Data redundancy and Data inconsistency

Multiple applications often save identical data across different files. This is data redundancy.
When an update occurs in one file but not in another, it creates conflicting, out-of-sync copies of the same information. this is data inconsistency.

e.g. The same student information may appear in multiple files. If he changes his branch from cse to ece then his info must be changed in all the places where his info is saved.
### Problem 2 — Difficult data access

Without dbms it becomes very difficult to access data from a large Database.
e.g.
Suppose the administrator asks:

> Find all CSE students out of 1000 whose marks are greater than 80.

With ordinary files, you may need to write a program specifically for this.

A DBMS allows something like:

```sql
SELECT *
FROM Student
WHERE Branch = 'CSE'
AND Marks > 80;
```
### Problem 3 — Security

Not everyone should have access to everything.

For example:

- Student → can see own marks
- Teacher → can update marks
- Account department → can access fees
- Administrator → broader access

A DBMS provides mechanisms for controlling this.

# Goals of DBMS

The major goals are:

| Goal              | Meaning                                    |
| ----------------- | ------------------------------------------ |
| Data storage      | Store large amounts of data                |
| Data retrieval    | Retrieve required information efficiently  |
| Data sharing      | Allow multiple users to access data        |
| Data security     | Prevent unauthorized access                |
| Data integrity    | Keep data correct and valid                |
| Reduce redundancy | Avoid unnecessary duplication              |
| Concurrency       | Allow multiple users simultaneously        |
| Backup & recovery | Recover data after failures                |
| Data independence | Separate applications from storage details |

Exactly. I’ll **group related concepts under the same numbered heading**, while keeping your content and structure intact. I’ll also make sentences slightly tighter where possible.

# 4. Database Languages

Database languages are used to communicate with a database.

The major categories are:

```
Database Languages
       │
       ├── DDL
       ├── DML
       ├── DQL
       ├── DCL
       └── TCL
```


## 4.1 DDL — Data Definition Language

DDL is used to **define or modify the structure of the database**.

Examples:

```
CREATE
ALTER
DROP
TRUNCATE
```

### CREATE

```
CREATE TABLE Student (
    id INT,
    name VARCHAR(50),
    age INT
);
```

Creates a table.

---

### ALTER

Changes the structure.

```
ALTER TABLE Student
ADD email VARCHAR(100);
```

---

### DROP

Deletes the database object.

```
DROP TABLE Student;
```

The table itself is removed.

---

### TRUNCATE

Removes all rows while keeping the table structure.

```
TRUNCATE TABLE Student;
```

---

## 4.2 DML — Data Manipulation Language

Used to manipulate data inside tables.

Common commands:

```
INSERT
UPDATE
DELETE
```

### INSERT

```
INSERT INTO Student
VALUES (101, 'Rahul', 20);
```

### UPDATE

```
UPDATE Student
SET age = 21
WHERE id = 101;
```

### DELETE

```
DELETE FROM Student
WHERE id = 101;
```

---

## 4.3 DQL — Data Query Language

Used to retrieve data.

The main command is:

```
SELECT
```

Example:

```
SELECT *
FROM Student;
```

Some textbooks classify `SELECT` under DML instead of treating DQL separately. **Don't get stuck on the classification; the important point is that SELECT retrieves data.**

---

## 4.4 DCL — Data Control Language

Controls permissions.

- G**RANT** — Gives users permissions to access or perform operations on database objects.
    - Example: giving a user permission to `SELECT` from a table.
- **REVOKE** — Removes permissions previously given to a user.
    - Example: removing a user's `SELECT` permission.
Commands:

```
GRANT
REVOKE
```

Example:

    ```
    GRANT SELECT ON Student TO User1;
    ```    
    → User1 can now view the `Student` table.
    
- **REVOKE** — Takes away permission.
    
	    ```
	    REVOKE SELECT ON Student FROM User1;
	    ```
    → User1 can no longer view the `Student` table.

---

## 4.5 TCL — Transaction Control Language

Controls transactions.

Important commands:

```
COMMIT
ROLLBACK
SAVEPOINT
```

- **COMMIT** — Permanently saves all changes made in the current transaction.
- **ROLLBACK** — Undoes changes made in the current transaction since the last `COMMIT` (or to a savepoint, if specified).
- **SAVEPOINT** — Creates a temporary point within a transaction to which you can later roll back

Example:

- **COMMIT** — Permanently saves changes.
    
	    ```
	    UPDATE Student SET age = 21 WHERE id = 1;
	    COMMIT;
	    ```
    
    → The change is permanently saved.
    
- **ROLLBACK** — Cancels/undoes changes.
    
	    ```
	    UPDATE Student SET age = 25 WHERE id = 1;
	    ROLLBACK;
	    ```
    
    → The age goes back to its previous value.
    
- **SAVEPOINT** — Creates a point you can roll back to.
    
	    ```
	    SAVEPOINT sp1;
	    ```
    
    → Creates a checkpoint named `sp1`.
    
    Later:
    
	    ```
	    ROLLBACK TO sp1;
	    ```
    
    → Undoes changes made **after** `sp1`.

# 5. Database Users

Different people interact with a database in different ways.

```
                 DATABASE USERS
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
    DBA            Developers       End Users
       │
       └── Database Designers
```

---

## 5.1 Database Administrator — DBA

The **DBA** is responsible for managing the database system.

Responsibilities include:

- Creating databases
- Managing users
- Security
- Backup
- Recovery
- Performance tuning
- Storage management
- Access control
- Maintaining database availability

Think of DBA as the **administrator of the database system**.

---

## 5.2 Database Designers

They design the structure of the database.

They decide:

```
What entities exist?
        ↓
What attributes do they have?
        ↓
How are entities related?
        ↓
What constraints exist?
```

For a college:

```
Student
Course
Teacher
Department
```

and relationships such as:

```
Student ── enrolls ── Course
Teacher ── teaches ── Course
```

---

## 5.3 Application Programmers

They develop applications that communicate with the DBMS.

For example:

```
React frontend
      ↓
Express backend
      ↓
SQL query
      ↓
Database
```

The backend developer may write:

```
SELECT * FROM Student;
```

---

## 5.4 End Users

These are people who use applications backed by databases.

Examples:

- Bank customers
- Students
- Teachers
- Online shoppers
- Employees

They may never directly write SQL.

# 6. Database Abstraction (Important Exam Concept)

A database hides enormous implementation details (such as how bytes are physically stored on a disk) from the user by providing different levels of abstraction.

The structural hierarchy flows as follows:

$$\text{User} \rightarrow \text{External Level} \rightarrow \text{Conceptual Level} \rightarrow \text{Internal Level} \rightarrow \text{Storage}$$

### 6.1 Physical / Internal Level

- **Definition:** The lowest level of abstraction.
    
- **Purpose:** Describes how data is physically stored on the disk (e.g., data blocks, indexes, files, and storage structures).
    
- **Note:** Users generally do not need to concern themselves with these details.

### 6.2 Logical / Conceptual Level

- **Definition:** Describes _what_ data is stored and the relationships between that data.
    
- **Example:** Defines tables and relations, such as:
    
    - `STUDENT` table structure (`Student_ID`, `Name`, `Age`, `Branch`)
        
    - Relationships like `STUDENT ─── enrolls ─── COURSE`
        
- **Note:** This level is independent of exact disk blocks.
### 6.3 External / View Level

- **Definition:** The highest level of abstraction. Different users see customized, restricted views of the same underlying database.
    
- **Examples of User Views:**
    
    - **Student View:** Name, Course, Marks
        
    - **Accounts View:** Name, Student_ID, Fees, Payment_Status
        
    - **Teacher View:** Student_ID, Name, Marks, Attendance
        

# 7. Database Architecture

Depending on the syllabus, database architecture covers two primary perspectives: **Three-Schema Architecture** and **Tier/Client-Server Architecture**.

### 7.1 Three-Schema Architecture

Closely tied to database abstraction, it maps out three distinct schemas:

1. **External Schema:** User-specific views.
    
2. **Conceptual Schema:** Overall logical structure.
    
3. **Internal Schema:** Physical storage structure.
    

### 7.2 Two-Tier Architecture

- **Definition:** A client application communicates directly with the database server.
    
- **Flow:** `Client Application ──> Database Server ──> Database`
    
- **Example:** `Desktop Application ──> MySQL`
    

### 7.3 Three-Tier Architecture

- **Definition:** Highly common in modern web applications, splitting logic across three layers.
    
- **Flow:** `Client ──> Application Server ──> Database Server`
    
- **Example:** `Browser / React ──> Express / Node.js ──> PostgreSQL`
    
- **Advantages:**
    
    - Better security
    - Easier maintenance
    - Better scalability
    - Clear separation of business logic from UI and database

## Important Relational Terminology

- **Relation:** A relation is essentially a **table**.
    
- **Tuple:** A tuple represents a single **row** in a relation.
    
    - _Example:_ `101 | Rahul | CSE | 20` is one tuple.
        
- **Attribute:** An attribute represents a **column** in a relation.
    
    - _Example:_ `Student_ID`, `Name`, `Branch`, `Age`.
        
- **Domain:** The set of all permitted or valid values allowed for an attribute.
    
    - _Examples:_
        
        - `Age` $\rightarrow$ positive integers
            
        - `Branch` $\rightarrow$ `{CSE, ECE, EEE, ME}`
            
- **Degree:** The **number of attributes (columns)** in a relation.
    
    - _Example:_ If a relation has 4 attributes (`Student_ID`, `Name`, `Branch`, `Age`), its **degree = 4**.
        
- **Cardinality:** The **number of tuples (rows)** in a relation.
    
    - _Example:_ If a table contains 100 students, its **cardinality = 100**.
        

### 💡 Easy Memory Trick

- **Degree** $\rightarrow$ **C**olumns (both start with consonants or use the alphabetical flow, but remember: Degree = Columns)
    
- **Cardinality** $\rightarrow$ **R**ows (or think of Cardinality counting the items)
# 10. Relational Database Constraints

Constraints are rules that data must follow to prevent invalid data from entering the database. They are categorized into four major types: **Domain Constraint, Key Constraint, Entity Integrity, and Referential Integrity**.

### 10.1 Domain Constraint

- **Definition:** Each attribute must contain values exclusively from its permitted domain.
- **Example:**  
    - Attribute: `Age` (must be an integer)
    - `Age = 20` (Valid)
    - `Age = 25` (Valid)
    - `Age = "Hello"` (Invalid)

### 10.2 Key Constraint

- **Definition:** A key should uniquely identify tuples according to the type of key being used.
- **Example:** `Student_ID` should uniquely identify a student (e.g., 101 for Rahul, 102 for Priya, 103 for Amit). Two students cannot share the same `Student_ID` if it is designated as the primary key.

### 10.3 Entity Integrity Constraint

- **Definition:** The **primary key cannot be NULL**.  
- **Reason:** Every row must be uniquely identifiable. If a primary key is NULL (e.g., `Student_ID = NULL`, `Name = Rahul`), the database cannot determine which specific student the row represents.
### 10.4 Referential Integrity Constraint

- **Definition:** This constraint applies to foreign keys to maintain consistency between related tables.
- **Example Structure:**
    - **DEPARTMENT:** `Dept_ID` (10, 20), `Dept_Name` (CSE, ECE)
    - **STUDENT:** `Student_ID`, `Name`, `Dept_ID` (Foreign key referencing `DEPARTMENT.Dept_ID`)
- **Rule:** You cannot insert a foreign key value that does not exist in the parent table (e.g., inserting `Student_ID = 103` with `Dept_ID = 99` would violate referential integrity if department 99 does not exist).

## Keys in Relational Databases

Keys are extremely important components of relational databases, categorized into six major types: **Super Key, Candidate Key, Primary Key, Alternate Key, Foreign Key, and Composite Key**.

### 11.1 Super Key

- **Definition:** Set of attributes that uniquely identifies a row in a relation.
- **Example:** Given attributes `{ID, Email, Name}`, possible super keys include:
    
    - `{ID}`
    - `{Email}`
    - `{ID, Name}`
    - `{ID, Email}`
    - `{ID, Email, Name}`
        
- **Reason:** Each combination contains enough information to uniquely identify the row.
### 11.2 Candidate Key

- **Definition:** A **minimal** super key (a super key with no redundant attributes).
- **Example:** If `{ID}` and `{Email}` both uniquely identify a student on their own, both are candidate keys. However, `{ID, Name}` is _not_ a candidate key because `{ID}` alone is already sufficient.
### 11.3 Primary Key

- **Definition:** A specific candidate key chosen by the database designer to uniquely identify tuples in a table.
- **Properties:**
    - Must be **Unique**
    - **Cannot be NULL**
    - Uniquely identifies each row

### 11.4 Alternate Key

- **Definition:** Candidate keys that were **not** selected as the primary key but they can also uniquely identify the tuple.
- **Example:**
    
    - Candidate keys: `{Student_ID}`, `{Email}`
    - Primary Key: `Student_ID`
    - Alternate Key: `Email`

### 11.5 Foreign Key

- **Definition:** An attribute (or set of attributes) in one relation that references the primary key of another relation.
    
- **Example:**
    
    - **`STUDENT` table:** `Student_ID`, `Name`, `Dept_ID` (Foreign Key)
    - **`DEPARTMENT` table:** `Dept_ID` (Primary Key), `Dept_Name`
### 11.6 Composite Key

- **Definition:** A primary key or candidate key consisting of **multiple attributes** combined to uniquely identify a row.
    
- **Example:** In an `ENROLLMENT` table (`Student_ID`, `Course_ID`, `Grade`), neither `Student_ID` nor `Course_ID` alone can uniquely identify an enrollment row. Together, the pair **`(Student_ID, Course_ID)`** forms a composite key.

#  ER Model

The **Entity-Relationship (ER) model** is a conceptual blueprint of a database used before implementation. It represents **entities, attributes, relationships, and constraints**.

## 1. Some useful terms
### 1.1 Entity

An **entity** is a distinguishable real-world object.
**Examples:** Student, Teacher, Course, Department, Employee, Product, Customer.

- **Entity Type:** Category of entities, e.g., `Student`.
- **Entity Instance:** Individual entity, e.g., `Rahul`.
### 1.2 Entity Set

An **entity set** is a collection of similar entities.
**Example:** The `Student` entity set may contain Rahul, Priya, and Amit.

### 1.3 Attributes

**Attributes** describe the properties of an entity.
**Example:** A `Student` may have:
`Student_ID, Name, Age, Email, Branch`

#### 1.3.1 Types of Attributes

- **Simple Attribute:** Cannot be divided further.  
    _Example:_ `Age`
- **Composite Attribute:** Can be divided into smaller attributes.  
    _Example:_ `Name → First_Name, Last_Name`  
    _Example:_ `Address → Street, City, State, PIN`
- **Single-Valued Attribute:** Has only one value for each entity.  
    _Example:_ `Date_of_Birth`
- **Multi-Valued Attribute:** Can have multiple values for an entity.  
    _Example:_ `Phone_Number`
- **Derived Attribute:** Calculated from another attribute.  
    _Example:_ `Age` derived from `Date_of_Birth`
- **Stored Attribute:** Actually stored in the database.  
    _Example:_ `Date_of_Birth`

### 1.4 ER Diagram Symbols

|Component|Symbol|
|---|---|
|Entity|Rectangle|
|Weak Entity|Double Rectangle|
|Relationship|Diamond|
|Attribute|Oval|
|Key Attribute|Underlined Oval|
|Multivalued Attribute|Double Oval|
|Derived Attribute|Dashed Oval|

## 2. Relationships

### 2.1 Relationship

A **relationship** represents an association between entities.

**Examples:**

`Student ─── enrolls in ─── Course`
`Employee ─── works_for ─── Department`

### 2.2 Relationship Set

A **relationship set** is a collection of similar relationship instances.
**Example:** Multiple student-to-course enrollments form the `ENROLLS` relationship set.

### 2.3 Degree of Relationship

The **degree** indicates the number of entity types participating in a relationship.

- **Unary (Recursive) Relationship:** One entity type participates.  
    _Example:_ An employee supervises another employee.
- **Binary Relationship:** Two entity types participate.  
    _Example:_ `Student ─── enrolls in ─── Course`  
    **Degree = 2**
- **Ternary Relationship:** Three entity types participate.  
    _Example:_ `Supplier ─── supplies ─── Product ─── to ─── Project`  
    **Degree = 3**

## 3. Constraints

### 3.1 Mapping Cardinality

**Mapping cardinality** specifies how many entities can participate in a relationship.

- **One-to-One (1:1):** One entity is associated with at most one entity on the other side.  
    _Example:_ `Person ─── has ─── Passport`
    
- **One-to-Many (1:N):** One entity can be associated with many entities.  
    _Example:_ `Department 1 ─── N Employee`
    
- **Many-to-One (N:1):** The same relationship viewed from the opposite direction.  
    _Example:_ `Employee N ─── 1 Department`
    
- **Many-to-Many (M:N):** Many entities on both sides can be associated.  
    _Example:_ `Student M ─── N Course`
### 3.2 Participation Constraints

- **Total Participation:** Every entity **must** participate in the relationship. Represented by a **double line**.  
    _Example:_ Every employee must belong to a department.

- **Partial Participation:** Participation is **optional**. Represented by a **single line**.  
    _Example:_ Not every employee manages a department.
## 4. Weak Entity

A **weak entity** cannot be uniquely identified using its own attributes alone. It depends on an **owner/strong entity** for identification.

**Example:** A `Dependent` may be identified using: `Employee_ID + Dependent_Name`
### 4.1 Strong vs Weak Entity

|Strong Entity|Weak Entity|
|---|---|
|Has its own primary key|Does not have a complete key of its own|
|Exists independently|Depends on an owner entity|
|Represented by a rectangle|Represented by a double rectangle|

## 5. Mapping ER Model to Relational Model

The ER model is converted into **relational tables** using specific mapping rules.
**ER Model → Mapping Rules → Relational Tables**

### 5.1 Mapping Strong Entity

For every strong entity, create a relation/table:

- Entity attributes → **Columns**
- Entity key → **Primary Key**

**Example:**

`STUDENT(Student_ID, Name, Age)`
**Primary Key:** `Student_ID`

### 5.2 Mapping 1:1 Relationship

Place the **primary key of one entity** as a **foreign key** in the other entity's table.

**Example:**

`PASSPORT(Person_ID FK)`

### 5.3 Mapping 1:N Relationship

Place the **primary key of the 1-side** into the **N-side** as a foreign key.

**Example:**

`EMPLOYEE(Emp_ID, Name, Dept_ID FK)`

Here, `Dept_ID` references the `DEPARTMENT` table.

### 5.4 Mapping M:N Relationship

Create a **separate relation** containing the primary keys of both participating entities.

- Both keys become foreign keys.
    
- Together, they form a **composite primary key**.
    

**Example:**

`ENROLLMENT(Student_ID FK, Course_ID FK)`

**Primary Key:** `(Student_ID, Course_ID)`

### 5.5 Mapping Multivalued Attributes

Create a **separate table** containing:

- Owner entity's primary key → Foreign key
    
- Multivalued attribute
    
- Both together → Composite primary key
    

**Example:**

`STUDENT_PHONE(Student_ID FK, Phone_Number)`

**Primary Key:** `(Student_ID, Phone_Number)`

### 5.6 Mapping Weak Entity

Create a separate table for the weak entity.

- Owner entity's primary key → Foreign key
    
- Weak entity's partial key → included
    
- Together → Composite primary key
    

**Example:**

`DEPENDENT(Employee_ID FK, Dependent_Name, Relationship)`

**Primary Key:** `(Employee_ID, Dependent_Name)`