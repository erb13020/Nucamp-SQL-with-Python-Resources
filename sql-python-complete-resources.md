# SQL with Python Course - Complete Resources

## Week 1: Relational Data Modeling

### Learning Goal
This week, we will learn the foundations of SQL Databases by studying relational data modeling. This will help us build a solid base that we will need further in the course when we interact with Databases using SQL and Python and build back-end applications that use a SQL database. Understanding relational data modeling is crucial because it will allow us to more efficiently and effectively utilize SQL databases.

### Learning Objectives
* Install Docker Desktop
* Use Docker to set up a "containerized" version of a PostgreSQL database and a pgAdmin interface
* Learn about foundational relational database concepts, such as relationships, primary and foreign keys, and restraints
* Read and create database models using an Entity Relational Diagram (ERD)
* Write SQL Code to implement a relational database based on an ERD

### Weekly Schedule
* Monday – Complete the Folders Setup, Docker Installation, and What is a Database? modules, then begin the module on Data Modeling.
* Tuesday – Complete the rest of the Data Modeling module, as well as the module on Integrity Constraints. Read the instructions for the Portfolio Project; begin brainstorming project ideas and working on your ER Diagram submission for this week.
* Wednesday – Complete the modules titled Tables and begin the module titled Docker, Postgres, and psql.
* Thursday – Complete the module on Docker, Postgres, and psql, and begin the final module for the week: Getting Started with SQL.
* Friday – Complete any remaining modules in the Lessons & Exercises section of this week, as well as the Quiz. Prepare for your workshop by reading the Week 1 Workshop Assignment instructions and watching the accompanying video -- but do not start the assignment yet! Complete your Portfolio Project submission for this week.

### Docker Installation
I want to make sure everyone has Docker installed and running on their systems. Please let me know if you are having trouble with Docker installation. Remember that this is a SQL course, not a Docker course (You will get plenty of that in your next DevOps course!). We just use this to make set up easier.

Here is a quick video I made going over the process:
https://www.youtube.com/watch?v=PnHzKswELG8

A few words of caution:
* Docker Desktop uses a lot of RAM. This can slow down your computer, especially if you have a lot of processes running or you don't have a lot of RAM. Consider pausing Docker Desktop when you are not coding.
* Docker may also flag anti-cheat systems in popular games like Overwatch, League of Legends, CS:GO. Docker uses a technology called Virtualization which gets flagged by these anti-cheat systems. Consider turning off virtualization when playing these games or using different computers for gaming and coding.

### Normalization Resources
Normalization is difficult to understand at first. Most people have a hard time understanding it the first time.

I've found these videos to be the most understandable on YouTube regarding normalization:
* Normalization Overview: https://www.youtube.com/watch?v=RZ9lvPRxwpg&list=PL_c9BZzLwBRK0Pc28IdvPQizD2mJlgoID&index=37
* First Normal Form: https://www.youtube.com/watch?v=JjwEhK4QxRo&list=PL_c9BZzLwBRK0Pc28IdvPQizD2mJlgoID&index=38

### Primary and Foreign Keys
Primary Key - a primary key is a restraint placed on a column (or combination of columns) in a table that uniquely identifies each record. It cannot contain null values and must be unique across all records in the table. A table must have one and only one primary key constraint, however, a primary key constraint can be placed on multiple columns.

Foreign Key - a foreign key is a restraint placed on a column in a table that references the primary key of another table. It is used to establish a relationship between the two tables.
| Tweets Table |  |  |  |  |  |  |
|--------------|---|---|---|---|---|---|
| tweet_id (PK) | timestamp | text | likes | retweets | user_id (FK) | first_name |
| 1 | 1615452013 | 20 Feb FIFA World Hi | 5 | 2 | 1 | john |
| 2 | 1602082023 | 20 Prem Game Tso | 5 | 1 | 2 | jane |
| 3 | 1581075024 | 20 Criss United Hi | 15 | 10 | 3 | kate |

| Users Table |  |  |  |  |
|------------|---|---|---|---|
| user_id (PK) | first_name | last_name | followers | following |
| 1 | john | smith | 12 | 15 |
| 2 | jane | doe | 51 | 41 |
| 3 | kate | white | 32 | 28 |

For example, consider this table tweets with a column called tweet_id which has a primary key restraint. The table also has a user_id column that stores the id of the user who tweeted the tweet. The user_id column has a foreign key restraint placed on it referring to the primary key of the users table. This establishes a many-to-one relationship between the two tables, allowing us to use the foreign key to find all tweets tweeted by a particular user.

Here is a great article on this important topic: https://learnsql.com/blog/why-use-primary-key-foreign-key/

### Entity Relationship Diagram and Relationships Key
| Concept | Notation |
|---------|----------|
| Attribute | Oval |
| Entity | Rectangle |
| Relationship | Diamond |
| Is-A Relationship | Triangle |
| Unique | Underlined Text |
| Participates 0 or more times | Line |
| Participates 1 or more times | **Bold line** |
| Participates at most once | Arrow |
| Participates once and only once | **Bold Arrow** |

| Cardinality Type | Diagram Representation | Description |
|-----------------|------------------------|-------------|
| Many-to-Many | ---- <> ---- | Multiple entities on both sides can be related to multiple entities on the other side |
| One-to-Many (or Many-to-One) | ---> <> ---- | One entity on one side can be related to multiple entities on the other side |
| One-to-One | ---> <> <--- | Each entity on one side is related to only one entity on the other side |
### Data Modeling Examples
To help you all get more comfortable with this vital concept, I've curated three articles that guide you through the creation of a data model for three different systems in order of complexity:

* Hotel Reservation System (Easy): https://vertabelo.com/blog/designing-a-data-model-for-a-hotel-room-booking-system/
* Online Job Portal (Medium): https://vertabelo.com/blog/designing-a-database-for-an-online-job-portal/
* Massively Multiplayer Online (MMO) Game (Difficult): https://vertabelo.com/blog/mmo-games-and-database-design/

### Social Media App Data Modeling
Every class, a few students choose to design a social media app for the week 1 portfolio project. One tricky model to implement is profiles following profiles. Here is a simplified diagram of how Twitter used to do it from the book Designing Data Intensive Applications:

## Users Table
| id | screen_name | profile_image |
|----|-------------|---------------|
| 12 | jack        | 1234567.jpg   |

## Follows Table
| follower_id | followee_id |
|-------------|-------------|
| 17055506   | 12          |

## Tweets Table
| id | sender_id | text               | timestamp     |
|----|-----------|--------------------| --------------|
| 20 | 12        | just setting up my twtr | 1142974214 |

1. We create a follows table with two attributes, follower_id and followee_id.
2. The primary key is the unique combination of follower_id and followee_id. That is, we place the primary key on both columns in the followers table.
3. Place a foreign key restraint on the follower_id column and have it reference either a user_accounts table or the users table.
4. Place a foreign key restraint on the followee_id column and have it reference the users table.

Here is another example where a profile can follow another profile (self-referencing many-to-many relationship):

## Profile Table
| id [PK] | tag          | age |
|---------|--------------|-----|
| 1       | @JayWhite    | 23  |
| 2       | @JohnSmith   | 44  |
| 3       | @SallyMae    | 53  |
| 4       | @JoeDoe      | 32  |
| 5       | @JaneDoe     | 29  |

## Follows Table
| follower_id [FK] | followee_id [FK] |
|-----------------|-----------------|
| 3               | 2               |
| 2               | 4               |
| 5               | 1               |
| 1               | 2               |

Source: Kleppmann, Martin. Designing Data Intensive Applications. 1st ed., O'Reilly, 2017
Link: https://github.com/ms2ag16/Books/blob/master/Designing%20Data-Intensive%20Applications%20-%20Martin%20Kleppmann.pdf

### Primary Key Conventions
In this course, we use the convention of surrogate primary keys on our tables. This means we place the primary key on the id column with a sequential integer (SERIAL datatype).

Another primary key convention is the natural primary key, where we find a column or combination of columns that are unique and not null, which can uniquely identify each row (UUID, social security number, email address, etc.)

Here is a great Stack Overflow post going over the differences between them:
https://stackoverflow.com/questions/36773011/what-is-the-difference-between-a-primary-key-and-a-surrogate-key

### Week 1 Kahoot
https://create.kahoot.it/share/week-1-pysql/a42cdc5c-cffe-4896-9219-16499d11b656

## Week 2: SQL Programming

### Learning Goal
This week, we will learn how to interact with relational databases. We will do this by creating, reading, updating, and deleting data using the SQL programming language.

The objective for this week is not to memorize every SQL command or to perfect your query-writing skills. Instead, we focus on exposing you to SQL and its functionalities in the context of a relational database. This exposure is crucial for understanding the foundational elements of back-end software engineering.

Most back-end engineers seldom have to write queries more complex than a simple INSERT, DELETE, or SELECT. However, having a strong understanding of SQL and relational databases provides an invaluable insight of how data is structured, accessed, and manipulated by the applications you will work on. This foundational knowledge will help you make informed decisions about database design, data manipulation, and even troubleshooting issues related to data storage and retrieval.

### Learning Objectives
* Create data using INSERT and CREATE TABLE statements
* Read data using SELECT queries with the proper use of aliases
* Update data using ALTER TABLE and UPDATE statements
* Delete data using DELETE, DROP, and TRUNCATE statements, including safely deleting records using the ON DELETE clause
* Using techniques such as SET operations, JOINs, subqueries, and CTEs to query multiple tables

### Weekly Schedule
* Monday – Complete the module on Database Manipulation.
* Tuesday – Complete the module on Database Queries: Using SELECT.
* Wednesday – Complete the module on Database Queries: Aggregations. Read the Portfolio Project instructions for this week and begin working on your submission.
* Thursday – Complete the module on Multi-Table Queries: Set Operations & Joins. Continue working on your Portfolio Project.
* Friday – Finish any remaining lessons and exercises, as well as any remaining Challenges and the Quiz. Aim to complete your Portfolio Project submission for this week prior to the Week 2 Workshop. Read the instructions for the Week 2 Workshop Assignment (but do not start it yet!).

### SQL Formatting
Please give this a read! I want you all to write clean formatted code!
https://learnsql.com/blog/24-rules-sql-code-formatting-standard/

You can also do this in Visual Studio using this extension. There are also a lot of other extensions to choose from.
https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools

### Generating Mock Data
When working with a relational database, it is often helpful to fill the database with mock data to use during development.

One way of accomplishing this is manually writing and executing multiple INSERT INTO statements.

A more efficient alternative is to use a tool to automatically generate test data and the INSERT INTO statements to insert the data into your database. Here's the link if you think this could be helpful: https://www.mockaroo.com/

A newer way of doing this is using generative AI. You can generate mock data for your table given a CREATE TABLE statement. You can use a prompt like this:

Please generate mock data for this PostgreSQL table created using this command using INSERT INTO:
```sql
CREATE TABLE employees ( 
     id SERIAL PRIMARY KEY, 
     name VARCHAR(100) NOT NULL, 
     salary NUMERIC
);
```

### JOIN vs SET Operations
I want to clear up any confusion between JOIN and SET operations:

JOIN OPERATIONS - Combines columns from two different tables into one table by fusing the primary key of one table with the corresponding foreign key of the other table. Operations include but are not limited to LEFT JOIN, RIGHT JOIN, OUTER JOIN, INNER JOIN, etc.

The big picture here is that you're combining the columns of two different tables.

SET OPERATIONS - Combine rows from two different queries based on a mathematical set operation to filter data. Operations include UNION, INTERSECT, and EXCEPT.

The important thing here is that you're combining the rows of two different queries.

# Database Query Set Operations

## 1. UNION
- Combines unique results from Query 1 and Query 2
- Removes duplicate rows
- Resulting set contains all distinct rows from both queries

## 2. UNION ALL
- Combines all results from Query 1 and Query 2
- Includes duplicate rows
- Total number of rows equals sum of rows from both queries

## 3. EXCEPT (or MINUS)
- Returns rows from Query 1 that are not in Query 2
- Removes any rows that exist in Query 2
- Shows unique elements in Query 1

## 4. INTERSECTION
- Returns only the rows that appear in both Query 1 and Query 2
- Shows common elements between the two queries

# SQL Join Types

## 1. LEFT JOIN
- Returns all records from Table A
- Matching records from Table B
- Unmatched records from Table A filled with NULL
```sql
SELECT *
FROM TableA 
LEFT JOIN TableB 
ON A.Key = B.Key
```

## 2. RIGHT JOIN
- Returns all records from Table B
- Matching records from Table A
- Unmatched records from Table B filled with NULL
```sql
SELECT *
FROM TableA
RIGHT JOIN TableB
ON A.Key = B.Key
```

## 3. INNER JOIN
- Returns only matching records
- Rows present in both tables
```sql
SELECT *
FROM TableA
INNER JOIN TableB
ON A.Key = B.Key
```

## 4. FULL OUTER JOIN
- Returns all records from both tables
- Matching and non-matching records
- Unmatched records filled with NULL
```sql
SELECT *
FROM TableA
FULL OUTER JOIN TableB
ON A.Key = B.Key
```

## 5. LEFT JOIN (Where B.Key is NULL)
- Returns records from Table A
- No matching records in Table B
```sql
SELECT *
FROM TableA
LEFT JOIN TableB
ON A.Key = B.Key
WHERE B.Key IS NULL
```

## 6. RIGHT JOIN (Where A.Key is NULL)
- Returns records from Table B
- No matching records in Table A
```sql
SELECT *
FROM TableA
RIGHT JOIN TableB
ON A.Key = B.Key
WHERE A.Key IS NULL
```

## Visual Representation
- Red: Records from Table A
- White: Records from Table B
- Overlapping area: Matching records

### SQL Aliases
Working with databases often requires us to fetch data from multiple tables, sometimes involving columns with identical names. This can make our SQL queries complex and hard to read. To improve clarity and manageability, SQL allows us to use aliases, which are temporary names assigned to tables or columns in our query.

Consider a scenario in a car database where we need to join two tables and both have a column named name. Without aliases, it becomes cumbersome to differentiate these columns:
```sql
SELECT
  person.name,
  car.name
FROM person
JOIN car
ON person.id = car.owner_id;
```

Here, aliases come to the rescue, making our query more readable and concise:
```sql
SELECT
  p.name AS person_name,
  c.name AS car_name
FROM person AS p
JOIN car AS c
ON p.id = c.owner_id;
```

In this revised query, p and c serve as shorthand for the person and car tables, respectively, and we explicitly rename the columns to avoid ambiguity. This not only enhances readability but also ensures our query results are clearly understood at a glance.

We can also use the new car_name and person_name aliases in other parts of our query. Suppose we want to order our results by car_name and person_name. Our query would look like this:
```sql
SELECT
  p.name AS person_name,
  c.name AS car_name
FROM person AS p
JOIN car AS c
ON p.id = c.owner_id
ORDER BY car_name, person_name
```

Here is a sample output of this query:
```
| person_name | car_name       |
|-------------|----------------|
| Alice Smith | Audi A4        |
| Bob Johnson | BMW 3 Series   |
| Carol Davis | BMW X5         |
| James Brown | Ford Mustang   |
| Emma Wilson | Honda Civic    |
| David Lee   | Honda Civic    |
| Michael Tan | Toyota Corolla |
| Sarah Jones | Toyota Prius   |
| Robert Chen | Tesla Model 3  |
| Lisa Wang   | Tesla Model Y  |
```

### SQL Best Practices
Tips on how to write better SQL from a FAANG data engineer:
https://youtu.be/nNR4jracHYA

More Best Practices on Writing SQL from Marc Lambeti:
https://www.linkedin.com/feed/update/urn:li:share:6968930637651013632?utm_source=linkedin_share&utm_medium=member_ios_link_share&utm_content=post

### Week 2 Kahoots
* Create, Update, and Delete: https://create.kahoot.it/share/week-2-create-update-delete/0e638a52-b0eb-4299-8d49-a042c384b0aa
* SELECT: https://create.kahoot.it/share/week-2-select/15c0d8af-0b02-49d2-916a-27c3b1301ea5

## Week 3: Python and Databases

### Learning Goal
This week, we will learn how to work with relational databases in Python. We will use object-relational mapping (ORM) to create back-end REST API servers that interact with these databases.

### Learning Objectives
* Configure a remote development environment in Visual Studio Code and develop applications within a Docker container
* Understand package management using Python and the PIP package manager
* Learn and implement database migrations
* Use an ORM tool to map tables in a relational database to class objects in Python and vice-versa as well as interact with a database using object oriented programming
* Inject SQL code into Python using a database adapter
* Comprehend the client-server relationship in a three-tier architecture, including URL structures, JSON data exchange, and HTTP methods, requests, and responses
* Build REST APIs using the Flask framework to perform CRUD operations on a relational database

Some students have found that there is an increase in difficulty for the third week. Make sure to get an early start so that you will be prepared for the workshop assignment.

We will also return to using object oriented design in Python. If you are still rusty on the object oriented paradigm, I suggest brushing up on these concepts including classes, member variables, class methods, and inheritance!

### Weekly Schedule
* Monday – You will learn how to set up a remote development environment in Visual Studio Code to develop inside a Docker container. Complete the books on Container Development and Python Packages. Complete the book on Database Migrations.
* Tuesday – Complete the book on Object-Relational Mapping (ORM). Read the Portfolio Project instructions for this week.
* Wednesday – Complete the Application Programming Interface book.
* Thursday – Begin the book Backend Application Development with Flask.
* Friday – Complete any remaining Lessons & Exercises for this week, as well as the Week 3 Quiz. Work on and submit your Portfolio Project report for this week. Read the Workshop 3 Assignment instructions and get ready for the Sunday workshop.

The workshop assignment directly builds on the exercises during the week. You must complete this week's exercises before starting the workshop.

### Python Code Formatting
This VS Code Extension is essential for clean python programming.

I would highly recommend using it for keeping your code up to https://pep8.org/ standards.
https://dev.to/adamlombard/how-to-use-the-black-python-code-formatter-in-vscode-3lo0

It's also available as a PIP package if you're using another IDE like Pycharm or if you don't prefer extensions:
https://pypi.org/project/black/

```
python -m pip install black
```

### How ORMs Work
The most important thing about ORMs for this week is that they provide a translation layer between a database and application code (python, javascript, etc).

An ORM allows databases to communicate with application code and vice versa.

Application code is object-oriented; our code comprises classes (objects) with member variables. On the other hand, our database comprises tables (entities/objects) with columns (attributes).

An ORM acts as a translation layer by:
1. Translating database tables to object-oriented classes (and vice versa)
2. Translating database columns to object-oriented member variables

Let's look at an example. Suppose we have a python app that keeps track of car inventory. We would like to use a database to store this data. So we create a table in our database for our car object:
```sql
CREATE TABLE cars (
    id SERIAL PRIMARY KEY,
    type VARCHAR(50),
    year INTEGER,
    make VARCHAR(50),
    model VARCHAR(50)
);
```

Since we write our app in Python, we normally create a Python class representing the car object:
```python
class Car:
    def __init__(self, car_type, year, make, model):
        self.type = car_type
        self.year = year
        self.make = make
        self.model = model
```

However, since we use an ORM to serve as a translation layer between our application code and database, we create the class using sqlalchemy - our ORM. This is also called a model:
```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class Car(db.Model):
    __tablename__ = 'cars'
    id = db.Column(db.Integer, primary_key=True)
    type = db.Column(db.String(50))
    year = db.Column(db.Integer)
    make = db.Column(db.String(50))
    model = db.Column(db.String(50))
```

The ORM would serve as a translation layer between the class Car and the table Car and member variables type, year, make, model, and columns type, year, make, and model.

In this code, we first import SQLAlchemy from flask_sqlalchemy and create an instance of SQLAlchemy named db. Then we define a Car class that inherits from db.Model to indicate that it is a SQLAlchemy model. We specify the table name using the __tablename__ attribute and define columns using db.Column. The id column is set as an Integer primary key with auto-incrementing behavior. The type, make, and model columns are set as String data type with a maximum length of 50 characters, while the year column is set as Integer data type.

Once you have defined the Car class, you can use it to interact with the database using SQLAlchemy's API. For example, to insert a new Car object into the database:
```python
new_car = Car(type='sedan', year=2022, make='Toyota', model='Camry')
db.session.add(new_car)
db.session.commit()
```

This creates a new Car object with the specified values for type, year, make, and model, adds it to the session, and commits the transaction to the database. To retrieve all Car objects from the database:
```python
cars = Car.query.all()
```

This returns a list of Car objects representing all rows in the cars table. These are just a couple of examples of how you can directly operate on your database within your application code using an ORM.

### Flask Resources
To help with learning Flask, here are some extra videos because backend engineering can be a pretty daunting topic to learn in one go:

1. Making Models with Flask-SQLAlchemy
https://www.youtube.com/watch?v=N7g6PQFRkf0

2. Performing CRUD operations with Flask
https://www.youtube.com/watch?v=3d8WE0yA-yA

Flask Application Structure
Video 1/2: https://youtu.be/q7PylhJAPQI

How To Write Flask Endpoints
Video 2/2: https://youtu.be/gJ8eNh9s8e8

This video does a great job explaining the REST API pattern:
https://youtu.be/SLwpqD8n3d0

### Week 3 Kahoots
* Migrations, ORM, Raw SQL: https://create.kahoot.it/share/week-3-servers-http-apis/5c206be2-18fa-40c3-9956-da400afe3c45
* Servers, HTTP, APIs: https://create.kahoot.it/share/week-3-servers-http-apis/5c206be2-18fa-40c3-9956-da400afe3c45

### Automatic Model Generation
Is it possible to automatically create models without having to define them in flask-sqlalchemy by creating a models.py file?

Yes! Here are a few resources that students have used in the past to automatically create models. Feel free to try them out in your portfolio project or free time:
* https://docs.sqlalchemy.org/en/14/orm/extensions/automap.html
* https://pypi.org/project/sqlacodegen/

## Week 4: Advanced PostgreSQL

### Learning Goal
This week, we will explore several advanced features of PostgreSQL. This includes but is not limited to database performance optimization, backups, provisioning, and analytics.

### Learning Objectives
* Store and interact with unstructured non tabular data in relational databases using JSON
* Optimize database performance using indexes while avoiding common performance antipatterns
* Explore database provisioning and backups, including the use of cloud-based platforms
* Perform an analytics workflow using SQL alongside the Python packages Numpy, Pandas, and Matplotlib

### Weekly Schedule
* Monday – Begin the module on Advanced SQL Techniques and complete it through the module Exercise: JSON Functions and Operators.
* Tuesday – Finish the module on Advanced SQL Techniques.
* Wednesday – Complete the modules on Optimization as well as Administration.
* Thursday – Begin the module on Data Visualization.
* Friday – Complete the module on Data Visualization. Complete your Portfolio Project and submit the final report. Read the instructions for the Week 4 Workshop Assignment.

### Advanced SQL Resources
Here's a few resources on Window Functions, an advanced SQL technique not covered in the course:
* https://youtu.be/9ybVbdQ9Z5k
* Mode also has an excellent technical blog: https://mode.com/sql-tutorial/sql-window-functions/

### Data Warehouses
Here's a good resource for data warehouses, an advanced application of SQL commonly used in Data Engineering (subset of Back-end engineering):
* Business standpoint explanation: https://youtu.be/VjlzuUzYJYM
* System design/architecture explanation: https://youtu.be/5XK_7QaP0fc

### Cloud Databases
Here is the official documentation for creating and connecting to a PostgreSQL database using Amazon's Relational Database Service (RDS). The other two major cloud providers (Microsoft Azure and Google Cloud Services) have similar setup wizards for their relational databases:
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html

### Authentication with JWT
You may have noticed that there were no login or logout endpoints in the assignment this week. As an additional challenge, consider implementing these features using JSON Web Tokens (JWT). JWT helps you securely handle user authentication by creating a token—a small piece of data—that proves a user is who they say they are. When a user logs in, the server gives them this token. The user then sends this token back to the server with each request to show they're authorized. This way, the server doesn't need to remember who's logged in, making the process simpler and more efficient for beginners like you to implement.

Here is the official introduction and documentation: https://jwt.io/introduction

### Data Engineering
Web development isn't the only discipline in software engineering! If you enjoyed this course, you may find the field of data engineering interesting:
https://www.youtube.com/watch?v=oUhpTxVi_PU

### Week 4 Kahoot
https://create.kahoot.it/share/week-4-advanced-sql/07f2f4a5-4f50-48d8-9185-24db962fa2e2a92
