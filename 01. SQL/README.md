# SQL

## Objectives

  * List the various features of a SQL database: e.g. Tables, Indexes, Migrations, and Joins
  * Compare and Contrast SQL/Relational/Table-based and NoSQL/Schemaless/Document-based databases
  * Write the SQL to create tables, columns, and rows
  * Write basic SQL queries

## Background

Pronouncd: "ess-que-el" or "sequel" - SQL is the language used with table-based, relational databases such as MySQL, SQLite, and PostgreSQL.

SQL was initially developed at IBM by Donald D. Chamberlin and Raymond F. Boyce in the early 1970s. This version, initially called SEQUEL (Structured English Query Language).

"SQL is a domain-specific language used in programming and designed for managing data held in a relational database management system. [SQL -Wikipedia](https://en.wikipedia.org/wiki/SQL)

SQL is incredibly powerful. It can be used to write virtually any query you can think of, as long as you have the data. 

## Tabular

All the data in a relational or SQL database is tabular, like an excel spreadsheet:

| id | name  | email | age |
| -- | ----  | ------| ------ |
| 1  | Bob   | bob@bob.com  | 34  |
| 2  | Sally | sally@sally.com  | 87  |
| 3  | Nick | nick@nick.com  | 20  |

## Why Learn SQL?

SQL/Relational databases are enormously prevalent, more common in fact than Schemaless/NoSQL/Document-based databases, and SQL is the language you use to communicate with virtually any relational database. 

Even stacks that use noSQL databases operationally, will often still maintain a SQL database for reporting purposes bc it is so fast and reliable.

Let's look at some of the simplest SQL commands.

### The Schema

A SQL database is different from a NoSQL database primarily in that it has a schema that we have to build before we can save data to it.

![schema](assets/sql-model.jpg)

### Basic SQL Commands

1. Read the data  --  **SELECT**
1. Insert new data  --  **INSERT**
1. Update existing data  --  **UPDATE**
1. Remove data  --  **DELETE**

What does this remind you of...? (CRUD!)

### SELECT

```sql
SELECT column-names
FROM table-name
WHERE condition
ORDER BY sort-order
```

e.g. 

```sql
SELECT FirstName, LastName, City, Country 
FROM Customer
WHERE City = 'Paris'
ORDER BY LastName
```

### INSERT

```sql
INSERT table-name (column-names)
VALUES (column-values)
```

e.g.

```sql
INSERT Supplier (Name, ContactName, City, Country)
VALUES ('Oxford Trading', 'Ian Smith', 'Oxford', 'UK')
```

### UPDATE

```sql
UPDATE table-name
SET column-name = column-value
WHERE condition
```

e.g.

```sql
UPDATE OrderItem
SET Quantity = 2
WHERE Id = 388
```

### DELETE

```sql
DELETE table-name
WHERE condition
```

e.g.

```sql
DELETE Customer
WHERE Email = 'alex@gmail.com'
```

## Advanced Commands

### Indexes

Another feature of SQL databases is the definition of **indexes** to speed up queries. Databases uses data structures like B-Trees to make column values fast to look up.

Read this [StackOverflow question](https://stackoverflow.com/questions/2955459/what-is-an-index-in-sql) to get a better idea of what a SQL index is.

### Joins - `JOIN`

SQL has many advanced query commands, but for our purposes we are just going to focus on one: the JOIN and its variants.

**Types of Joins**

1. (INNER) JOIN: Select records that have matching values in both tables.
1. LEFT (OUTER) JOIN: Select records from the first (left-most) table with matching right table records.
1. RIGHT (OUTER) JOIN: Select records from the second (right-most) table with matching left table records.
1. FULL (OUTER) JOIN: Selects all records that match either left or right table records.

![sql-joins](assets/sql-joins.png)

**Creating a JOIN example**

```sql
create index IndexCustomerName on Customer (
LastName ASC,
FirstName ASC
)
go
```

**JOIN Examples**

```sql
-- List all orders with customer information 

SELECT OrderNumber, TotalAmount, FirstName, LastName, City, Country
  FROM [Order] JOIN Customer
    ON [Order].CustomerId = Customer.Id
```

e.g.

```sql
-- List all orders with product names, quantities, and prices 

SELECT O.OrderNumber, CONVERT(date,O.OrderDate) AS Date, 
       P.ProductName, I.Quantity, I.UnitPrice 
  FROM [Order] O 
  JOIN OrderItem I ON O.Id = I.OrderId 
  JOIN Product P ON P.Id = I.ProductId
ORDER BY O.OrderNumber
```

## SQL Challenges - todofactory

1. Examine the database and schema code in the `sample db` folder. Can you identify what each part of the files do?
1. With a partner construct 5 of your own simple queries for the dofactory sandbox and run them. For reference for this schema scroll up to the image above or look at [this page](http://www.dofactory.com/sql/tutorial) of their tutorial e.g:
  
  - Return all customers: `SELECT * from Customer`
  - Return all orders: `SELECT * from Order`

1. Use dofactory's [SQL Sandbox](http://www.dofactory.com/sql/sandbox) to run the example JOIN queries. 
1. Write SQL queries for the psuedocode in `bank.sql` file.

## Strech Challenges

1. Watch this great [TED talk on data visualization](https://www.ted.com/talks/david_mccandless_the_beauty_of_data_visualization)
1. Construct 3 JOIN queries for the dofactory sql sandbox and run it.
1. Review the types of Joins. With a partner come up with one hypothetical query (in English/psuedocode) that exemplifies each one. Share your queries with another two pairs.
