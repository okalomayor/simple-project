# Project Report: Simple Login System with Database Connectivity in Python

## Overview

This project implements a basic login system using Python and MySQL. The system provides functionalities for user registration and report generation by connecting to a MySQL database. Designed for simplicity and ease of use, the project aims to demonstrate foundational skills in database connectivity, user authentication, and data retrieval using Python's `mysql-connector` library.

## Project Objectives

- **Database Connectivity**: Establish a reliable connection to a MySQL database for storing and retrieving user data.
- **User Registration**: Implement a function to register new users, storing essential information in the database.
- **Report Generation**: Create a report function that retrieves and displays all users' information from the database, formatted in a readable format.

## System Design

The project follows a modular approach with the following main components:

1. **Database Connection**: Connects to the MySQL database to allow access to user information.
2. **Registration Function**: Collects and stores user credentials and other relevant details in the database.
3. **Report Generation Function**: Retrieves and displays all user records from the database, providing a simple report for analysis.

## Setup and Configuration

### Prerequisites

- **Python 3.x**
- **MySQL** (or equivalent database like MariaDB)
- **MySQL Connector for Python**: Install via `pip install mysql-connector-python`.

### Database Configuration

To set up the database:
1. Create a MySQL database named `general_hospital_information`.
2. Define a table `user_info` with the required fields (e.g., `facility_id`, `hospital_type`, etc.).
3. Adjust the connection parameters (host, username, password, and database) in the code to match your database configuration.

### Code Walkthrough

The project’s Python code consists of the following main parts:

#### 1. Import Libraries and Connect to Database

```python
import mysql.connector
from getpass import getpass
```

The `mysql.connector` library handles MySQL database operations, while `getpass` is used to securely enter user passwords.

#### 2. Database Connection Function

```python
def connect_to_database():
    global mydb
    mydb = mysql.connector.connect(
        host="127.0.0.1",
        username="root",
        password="your_password",
        database="general_hospital_information"
    )
```

This function establishes a connection to the MySQL database and assigns it to a global variable `mydb`.

#### 3. User Registration

```python
def register():
    if mydb is None:
        print("Database connection is not established.")
        return
    username = input("Enter username: ")
    password = getpass("Enter password: ")
    cursor = mydb.cursor()
    sql = "INSERT INTO user_info (facility_id, hospital_type) VALUES (%s, %s)"
    val = (10001, 'Southeast Health Medical Center')
    cursor.execute(sql, val)
    mydb.commit()
    print("User registered successfully!")
```

The `register` function prompts for user credentials, inserts a new record into the `user_info` table, and confirms registration.

#### 4. Report Generation

```python
def generate_report():
    if mydb is None:
        print("Database connection is not established.")
        return
    cursor = mydb.cursor()
    cursor.execute("SELECT * FROM user_info")
    result = cursor.fetchall()
    for row in result:
        print(row)
```

The `generate_report` function retrieves and displays all user records from the `user_info` table.

#### 5. Execution of Functions

The script initiates a database connection and calls the `register` and `generate_report` functions sequentially.

```python
# Connect to the database
connect_to_database()

# Call the functions after the database connection is established
register()
generate_report()
```

## Results

Sample output for registration and report generation functions:

```plaintext
Enter username: okalp
Enter password: ········
User registered successfully!
(10001, 'Southeast Health Medical Center', 'yes', 'good')
...
(10026, 'Southeast Health Medical Center', 'no', 'bad')
...
```

This output indicates successful user registration and the ability to generate a report with user data.

## Conclusion

The project successfully demonstrates how to create a basic login and reporting system using Python and MySQL. Key takeaways include:
- Understanding how to manage database connections.
- Writing simple registration and report generation functions.
- Displaying data from the database in a structured format.

## Future Improvements

Potential enhancements for this project could include:
1. **Password Hashing**: Securely store user passwords with hashing.
2. **User Authentication**: Add a login validation system.
3. **Enhanced Report Generation**: Format and structure reports for readability.

Overall, this project is an excellent starting point for anyone interested in building a basic user authentication system with database connectivity in Python.
