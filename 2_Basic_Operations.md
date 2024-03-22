# Python Tutorial: Basic Operations with PyODBC

## Module 2: Basic Operations

In this module, we'll cover the fundamental operations you need to perform when working with databases using PyODBC. We'll learn how to execute SQL queries, fetch data from tables, and handle errors encountered during database operations.

### Executing SQL Queries

SQL (Structured Query Language) is the standard language for interacting with relational databases. PyODBC allows us to execute SQL queries easily within Python. Let's start by establishing a connection to a database:

```python
import pyodbc

# Establish a connection to the database
connection = pyodbc.connect('DSN=your_datasource_name;UID=username;PWD=password')

# Create a cursor object to execute queries
cursor = connection.cursor()

# Execute a simple SQL query
cursor.execute("SELECT * FROM your_table")

# Fetch the results
rows = cursor.fetchall()

# Print the results
for row in rows:
    print(row)
```

### Fetching Data

After executing a query, we need to fetch the data returned by the query. PyODBC provides methods like `fetchone()` and `fetchall()` to retrieve data:

- `fetchone()`: Fetches the next row of a query result set, returning a single sequence, or `None` when no more data is available.
- `fetchall()`: Fetches all remaining rows of a query result set as a list of tuples.

```python
# Fetch one row at a time
row = cursor.fetchone()
print(row)

# Fetch all rows at once
rows = cursor.fetchall()
for row in rows:
    print(row)
```

### Error Handling

Error handling is crucial when working with databases to gracefully handle unexpected situations. PyODBC allows us to catch and handle errors that may occur during database operations:

```python
try:
    # Attempt to execute a query
    cursor.execute("SELECT * FROM non_existent_table")
    rows = cursor.fetchall()
except pyodbc.Error as e:
    # Handle the error
    print(f"An error occurred: {e}")
```

Common errors that can occur include database connection errors, query syntax errors, or database constraint violations. By catching these errors, we can provide meaningful feedback to the user or take appropriate action to handle the situation.
