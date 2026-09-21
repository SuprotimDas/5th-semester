# 1. Relational Model

You know what is relational model.

# 2. The Catalog
- **The Catalog (Data Dictionary / Metadata Repository)**:  The **catalog** is also called the:

- Data dictionary
- System catalog
- Metadata repository

It stores **information about the database**, rather than ordinary application data. The catalog provides the metadata necessary to interpret and execute the query.

Suppose you create:

```
CREATE TABLE STUDENT(
    RollNo INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);
```

The DBMS needs to remember things such as:

```
Table name → STUDENT
Columns → RollNo, Name, Age
Data types → INT, VARCHAR, INT
Primary key → RollNo
Constraints → ...
Indexes → ...
Views → ...
```

# 3. Keys

In module 1

# 4. Relational algebra

**Relational Algebra** is a **procedural query language**.

This is called the **closure property**:

$Relation→Operation→Relation$

For example:

```
STUDENT → selection → STUDENTS_MATCHING_CONDITION
```
- Operates on relations and outputs relations based on the **closure property** ($Relation \rightarrow Operation \rightarrow Relation$). It is procedural, specifying _how_ to obtain results.
    
- **Fundamental Operations**:
    
    1. **Selection ($\sigma$)**: Filters and chooses **rows** based on a condition ($\sigma_{condition}(Relation)$).
	    e.g. $σDept=′CSE′​(STUDENT)$
    2. **Projection ($\pi$)**: Selects specific **columns** ($\pi_{columns}(Relation)$).
	    e.g. $πName​(STUDENT)$
    3. **Union ($\cup$)**: Combines rows from two union-compatible relations, removing duplicates.
        e.g. $CSE STUDENTS∪ECE STUDENTS$
    4. **Set Difference ($(-)$)**: Finds rows present in one relation but not the other; non-commutative ($A - B \neq B - A$).
    5. **Cartesian Product ($\times$)**: Combines every rows of relation $A$ with every row of relation $B$ ($m \times n$ tuples).
	    e.g. $STUDENT×COURSE$

- **Additional Operations**:
    
    - **Rename ($\rho$)**: Renames a relation or its attributes.
        e.g. $ρS​(STUDENT)$
        
        renames `STUDENT` to `S`
    - **Intersection ($\cap$)**: Returns tuples common to both relations.
        
    - **Joins**: Combines related tuples based on conditions. Includes 
	    - **Theta Join** (uses any comparison operator like $<, >, =$); 
	    - **Equi Join** (uses strict equality $=$); 
	    - **Natural Join** (automatically joins on attributes with the same name/domains and drops duplicate columns);  
	    - **Outer Joins** (Left, Right, and Full Outer Joins which preserve non-matching tuples using `NULL`).
						        <u>General form</u>:$R\bowtie_{\theta}S$ (where θ is a condition)
    - **Division ($\div$)**: Useful for "ALL"-type queries (e.g., finding entities that satisfy all conditions, such as students who completed all required courses).

# 5. Relational Calculus

-Relational algebra is **procedural**.

-Relational calculus is **non-procedural/declarative**.

**Relational Algebra**

You say:

> First select this, then join this, then project that.

**Relational Calculus**

You say:

> I want tuples satisfying this condition.

The DBMS determines how to obtain them.

There are two forms:

1. Tuple Relational Calculus — TRC
2. Domain Relational Calculus — DRC

## Tuple Relational Calculus (TRC)

TRC uses **tuple variables**.

General form: $\{t\mid P(t)\}$

Meaning:

> Find all tuples `t` such that predicate `P(t)` is true.

Conceptually:

$\{t \mid t\in STUDENT \land t.Dept='CSE'\}$

Here:

```
t
```

is a tuple variable.

### TRC Example

Find names of CSE students.

$\{t.Name \mid t\in STUDENT \land t.Dept='CSE'\}$

Meaning:

> Give me the Name attribute of every tuple `t` belonging to STUDENT where Dept is CSE.

### TRC Logical Operators

TRC uses logical operators such as:

 - AND => $\land$
-  OR => $\lor$
 - NOT => $\neg$
 - Exists => $\exists$
 - For all => $∀$

Example:

> Find students older than 20 from CSE.

$\{t.Name\mid t\in STUDENT \land t.Dept='CSE' \land t.Age>20\}$

## Domain Relational Calculus (DRC)

DRC works with **domain variables**, meaning individual attribute values.

General form:

$\{<x_1,x_2,...,x_n>\mid P(x_1,x_2,...,x_n)\}$

Suppose:

```
STUDENT(RollNo, Name, Dept, Age)
```

We want names of CSE students.

Conceptually:

$\{<n>\mid \exists r,a (STUDENT(r,n,'CSE',a))\}$

Here:

```
r → RollNo
n → Name
a → Age
```
Unlike TRC, we aren't treating the entire row as a variable.

Suppose:

```
STUDENT(RollNo, Name, Department, Age)
```

### How to write DRC?

Question:

> Find the names of all students.

In TRC, we'd think:

```
T.Name
```

In DRC, we need a variable for every attribute because DRC works with individual values.

Let's create:

```
r → RollNo
n → Name
d → Department
a → Age
```

So we have:

STUDENT(r,n,d,a)

Now we want to **return only `n`**.

Therefore:

$\boxed{ \{<n>\mid \exists r,d,a\; STUDENT(r,n,d,a)\} }$

This looks scary, but let's translate it.

---
4. Read the Formula Like English

${<n>∣∃r,d,a  STUDENT(r,n,d,a)}\{<n>\mid \exists r,d,a\; STUDENT(r,n,d,a)\}$

Break it:

 **`<n>`**

What do we want to output?

```
Name
```

So:

```
<n>
```

means:

> Return the name.

---

 **`|`**

Means:

> such that

So:

```
<n> |
```

means:

> Return the name **such that...**

---

 **`∃ r,d,a`**

This means:

> There exist some values of `r`, `d`, and `a`.

Why do we need them?

Because a STUDENT tuple contains **four attributes**:

```
RollNo → r
Name → n
Department → d
Age → a
```

We only want to display `n`, so the other variables are just used to establish that a valid STUDENT tuple exists.

---

 **`STUDENT(r,n,d,a)`**

This means:

> `(r,n,d,a)` is a tuple in the STUDENT relation.

So the whole thing means:

> **Return `n` such that there exist a roll number, department, and age for which `(r,n,d,a)` is a student tuple.**

That's all.

---

 **Now Add a Condition**

Question:

> Find names of students whose age is greater than 20.

We still have:

```
r → RollNo
n → Name
d → Department
a → Age
```

We want:

```
n
```

And our condition is:

```
a > 20
```

Therefore:

${<n>∣∃r,d,a(STUDENT(r,n,d,a)∧a>20)}$
# 6. Integrity Constraints

**Integrity constraints** ensure database data remains correct, consistent, and valid.

The types of constraints are:
- Domain constraint
- Key constraint
- Entity integrity constraint
- Referential Integrity constraint
- General constraints

###  **Domain Integrity**: 
	Values must belong to the appropriate domain.

Example:

```
Age INT
```

You shouldn't insert:

```
Age = 'ABC'
```

You can also constrain values:

```
Age INT CHECK (Age >= 0)
```

### **Key Constraint**

Ensures that a **key uniquely identifies a tuple**.

Example:

```
RollNo INT UNIQUE
```

Two students cannot have the same `RollNo`.

This includes concepts like:

- Super key
- Candidate key
- Primary key


### **Entity Integrity**: 

Entity integrity says:

> A primary key cannot be NULL.

Why?

Because the primary key identifies the tuple.

If:

```
RollNo = NULL
```

you can't properly identify the student.

Example:

```
RollNo INT PRIMARY KEY
```
    
### **Referential Integrity**: 

Ensure that a foreign key should refer to an existing key value in the referenced table.

Suppose:

```
DEPARTMENT
DeptID = 1, 2, 3
```

And:

```
STUDENT.DeptID
```

is a foreign key.

You shouldn't normally insert:

```
Student DeptID = 99
```

if department 99 doesn't exist.

This prevents **orphan references**.

### General constraints
- **UNIQUE Constraint**: 
	Ensures values are unique.

```
Email VARCHAR(100) UNIQUE
```

Two students shouldn't have the same email if the column is intended to be unique.
    
- **NOT NULL Constraint**: Prohibits `NULL` entries to ensure mandatory fields are always filled.
    
- **CHECK Constraint**: Restricts data entries based on a specific logical condition (e.g., `Age INT CHECK(Age >= 18)`).
    
- **DEFAULT Constraint**: Automatically assigns a preset fallback value when no explicit value is provided (e.g.,` Status VARCHAR(20) DEFAULT 'Active'`).

# 7. Triggers
A **trigger** is a database program that automatically executes when a specified event occurs.

Think:

> **Event → Trigger → Automatic action**

Example:

```
Student inserted
       ↓
Trigger fires
       ↓
Audit record created
```

---

## Trigger Events

Triggers can be associated with events such as:

```
INSERT
UPDATE
DELETE
```

For example:

```
AFTER INSERT
AFTER UPDATE
BEFORE DELETE
```

Exact trigger capabilities vary by DBMS.

---

## Example Trigger

Suppose we have:

```
STUDENT
```

and:

```
STUDENT_LOG
```

Whenever a student is inserted, we want to record it.

Conceptually:

```sql
CREATE TRIGGER student_insert_log
AFTER INSERT ON STUDENT
FOR EACH ROW
INSERT INTO STUDENT_LOG
VALUES (NEW.RollNo, CURRENT_TIMESTAMP);
```

The exact syntax depends on the DBMS, but the concept is:

```
INSERT into STUDENT
        ↓
Trigger automatically executes
        ↓
STUDENT_LOG gets entry
```

---

## Uses of Triggers

Triggers are commonly used for:

### 1. Auditing

Track changes.

```
Who changed what?
When?
```

### 2. Maintaining derived data

Automatically update related information.

### 3. Enforcing business rules

For example:

```
salary cannot decrease
```

### 4. Logging

Record important events.

### 5. Automatic actions

Perform an action whenever a database event happens.

---

## Problems with Triggers

Triggers are powerful, but don't blindly use them.

Problems can include:

- Hidden side effects
- Harder debugging
- Unexpected chained operations
- Performance overhead
- Complex dependencies

A developer may execute:

```
UPDATE STUDENT ...
```

and not realize that several triggers execute additional operations.

That's why triggers should be used deliberately.

# 8. Views

A **view** is a virtual table based on a query.

Example:

```
CREATE VIEW CSE_STUDENTS AS
SELECT RollNo, Name
FROM STUDENT
WHERE Dept = 'CSE';
```

Now:

```
SELECT *
FROM CSE_STUDENTS;
```

The view behaves like a table from the user's perspective, but its definition is based on the underlying query.

Another example:

**STUDENT**

| RollNo | Name  | Dept | Age | Phone | Address |
| ------ | ----- | ---- | --- | ----- | ------- |
| 101    | Rahul | CSE  | 20  | 9876  | Kolkata |
| 102    | Amit  | CSE  | 22  | 8765  | Delhi   |
| 103    | Priya | ECE  | 21  | 7654  | Mumbai  |

Now imagine that teachers should be able to see:

```
RollNo
Name
Dept
```

but **not Phone or Address**.

You could repeatedly write:

```
SELECT RollNo, Name, Dept
FROM STUDENT;
```

But instead, create a view:

```
CREATE VIEW Student_Public AS
SELECT RollNo, Name, Dept
FROM STUDENT;
```

Now you can simply do:

```
SELECT *
FROM Student_Public;
```

Output:

|RollNo|Name|Dept|
|---|---|---|
|101|Rahul|CSE|
|102|Amit|CSE|
|103|Priya|ECE|

## Why Use Views?

### 1. Security

Suppose STUDENT has:

```
RollNo
Name
Age
Phone
Address
Salary
```

You don't want every user seeing everything.

Create:

```
CREATE VIEW STUDENT_PUBLIC AS
SELECT RollNo, Name, Age
FROM STUDENT;
```

Users can access the view without directly exposing sensitive columns.

### 2. Simplicity

Instead of repeatedly writing a complicated query:

```
SELECT ...
JOIN ...
WHERE ...
GROUP BY ...
```

create a view.

Then:

```
SELECT *
FROM my_view;
```

### 3. Abstraction

Users don't need to know the underlying table structure.

---

## View vs Table

|Table|View|
|---|---|
|Stores actual data|Usually stores query definition|
|Physical database object|Virtual/logical representation|
|Data exists independently|Depends on underlying tables|
|Can directly store rows|Results derived from underlying data|

There are also **materialized views** in some DBMSs, which physically store query results for performance. Don't confuse them with ordinary views.

---

## View Example with Join

Suppose:

```
STUDENT(RollNo, Name, DeptID)
DEPARTMENT(DeptID, DeptName)
```

Create:

```
CREATE VIEW STUDENT_DETAILS AS
SELECT
    STUDENT.RollNo,
    STUDENT.Name,
    DEPARTMENT.DeptName
FROM STUDENT
JOIN DEPARTMENT
ON STUDENT.DeptID = DEPARTMENT.DeptID;
```

Then:

```
SELECT *
FROM STUDENT_DETAILS;
```

---

## Can We Modify a View?

Sometimes yes.

Simple views may be **updatable**.

Complex views involving things such as:

- aggregation
- `GROUP BY`
- certain joins
- `DISTINCT`

may not be directly updatable, depending on the DBMS and query.

So don't memorize:

> "Views can never be updated."

That's false.

The correct idea is:

> **Some views are updatable; others aren't.**