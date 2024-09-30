---
id: SQL
aliases: []
tags: []
---

SQL is a domain-specific language used in programming and managing data held in relational database management systems (RDBMS). It was first developed in the 1970s at IBM and has since become the standard for working with relational databases.

SQL allows users to:

    Insert new data
    Query data
    Update existing data
    Delete data
    Manage databases and tables (creating, altering, and dropping)
    Manage database users and permissions

```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(100)
);

ALTER TABLE employees ADD COLUMN age INT;

INSERT INTO employees (id, name, department) VALUES (1, 'Alice', 'HR');
 
UPDATE employees SET department = 'IT' WHERE id = 1;

DELETE FROM employees WHERE id = 1;


```


## Data Control Language (DCL):

Used to control access to data.

- GRANT: Grants user access to the database.

```sql
GRANT SELECT, INSERT ON employees TO 'user';
```

- REVOKE: Removes user access.

```sql
REVOKE INSERT ON employees FROM 'user';
```

## Transaction Control Language (TCL):

Used to manage transactions in the database.

- BEGIN TRANSACTION: Starts a transaction.

- COMMIT: Saves all changes made during the transaction.

```sql
COMMIT;
```

- ROLLBACK: Reverts all changes if an error occurs.

```sql
ROLLBACK;
```

## Common SQL Databases

Several relational database management systems use SQL as their primary language:

- MySQL: Open-source and widely used for web development.
- PostgreSQL: Open-source and highly standards-compliant, with advanced features like JSON support.
- SQLite: A lightweight, file-based database often used in embedded applications.
- Microsoft SQL Server: Developed by Microsoft, commonly used in enterprise environments.
- Oracle Database: A widely used database for enterprise applications, especially for large-scale systems.


