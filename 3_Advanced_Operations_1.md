# Python Tutorial: Advanced Operations with PyODBC

## Module 3: Advanced Operations

In this module, we will cover some advanced operations that can be performed using PyODBC, including parameterized queries, transactions, and bulk data operations. These topics are essential for efficient and secure database operations in Python.

### 1. Parameterized Queries

#### Importance of Parameterized Queries

Parameterized queries are essential for security and efficiency when working with databases. They help prevent SQL injection attacks by separating SQL code from user input. Additionally, parameterized queries can improve performance by allowing the database to reuse query plans.

#### Executing Parameterized Queries with PyODBC

PyODBC provides a simple way to execute parameterized queries. Here's how you can do it:

```python
import pyodbc

# Establish a connection to the database
conn = pyodbc.connect('DRIVER={DriverName};SERVER=ServerName;DATABASE=DatabaseName;UID=Username;PWD=Password')

# Create a cursor
cursor = conn.cursor()

# Define the SQL query with parameters
sql_query = "SELECT * FROM table_name WHERE column_name = ?"

# Execute the query with parameters
cursor.execute(sql_query, ('parameter_value',))

# Fetch and print the results
for row in cursor.fetchall():
    print(row)

# Close the cursor and connection
cursor.close()
conn.close()
```

### 2. Transactions

#### Understanding Transactions

In the context of databases, a transaction is a sequence of database operations that are treated as a single unit of work. Transactions ensure data integrity and consistency by either committing all changes or rolling back to the previous state if an error occurs.

#### Managing Transactions with PyODBC

PyODBC allows you to manage transactions using the `commit()` and `rollback()` methods. Here's how you can use transactions:

```python
import pyodbc

# Establish a connection to the database
conn = pyodbc.connect('DRIVER={DriverName};SERVER=ServerName;DATABASE=DatabaseName;UID=Username;PWD=Password')

# Create a cursor
cursor = conn.cursor()

try:
    # Begin a transaction
    conn.autocommit = False

    # Execute SQL statements within the transaction
    cursor.execute("UPDATE table_name SET column_name = 'new_value' WHERE condition")

    # Commit the transaction if all statements succeed
    conn.commit()
    print("Transaction committed successfully!")

except Exception as e:
    # Roll back the transaction if an error occurs
    conn.rollback()
    print("Transaction rolled back due to error:", e)

finally:
    # Restore autocommit mode and close cursor and connection
    conn.autocommit = True
    cursor.close()
    conn.close()
```

### 3. Bulk Data Operations

#### Performing Bulk Data Operations with PyODBC

PyODBC provides efficient ways to perform bulk data operations such as bulk inserts and updates. This can significantly improve performance when dealing with large datasets. Here's an example of bulk insert operation:

```python
import pyodbc

# Establish a connection to the database
conn = pyodbc.connect('DRIVER={DriverName};SERVER=ServerName;DATABASE=DatabaseName;UID=Username;PWD=Password')

# Create a cursor
cursor = conn.cursor()

try:
    # Begin a transaction
    conn.autocommit = False

    # Execute bulk insert operation
    rows = [(value1, value2), (value3, value4), ...]  # List of tuples containing values for insertion
    cursor.executemany("INSERT INTO table_name (column1, column2) VALUES (?, ?)", rows)

    # Commit the transaction if all inserts succeed
    conn.commit()
    print("Bulk insert operation completed successfully!")

except Exception as e:
    # Roll back the transaction if an error occurs
    conn.rollback()
    print("Bulk insert operation failed:", e)

finally:
    # Restore autocommit mode and close cursor and connection
    conn.autocommit = True
    cursor.close()
    conn.close()
```