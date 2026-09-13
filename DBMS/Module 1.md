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
