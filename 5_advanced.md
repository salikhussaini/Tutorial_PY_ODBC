# Python Tutorial: Advanced Database Operations with PyODBC

## Module 7: Advanced Topics (Optional)

In this module, we'll delve into advanced database operations using PyODBC, covering topics such as calling stored procedures and functions, implementing connection pooling for better resource management, and exploring how to work with NoSQL databases using PyODBC.

### 1. Stored Procedures and Functions

#### What are Stored Procedures and Functions?
Stored procedures and functions are precompiled SQL queries that are stored in the database and can be executed by calling their names. They are commonly used for performing complex operations or computations on the database server itself.

#### Calling Stored Procedures and Functions with PyODBC
PyODBC provides a simple way to call stored procedures and functions from Python. Here's a basic example:

```python
import pyodbc

# Establish a connection to the database
conn = pyodbc.connect('DSN=your_dsn;UID=username;PWD=password')

# Create a cursor object
cursor = conn.cursor()

# Example of calling a stored procedure
cursor.execute("{CALL your_stored_procedure_name(param1, param2)}")

# Fetch the result if needed
result = cursor.fetchall()

# Close the cursor and connection
cursor.close()
conn.close()
```

Replace `your_dsn`, `username`, `password`, and `your_stored_procedure_name` with your actual DSN (Data Source Name), database credentials, and the name of your stored procedure.

### 2. Connection Pooling

#### What is Connection Pooling?
Connection pooling is a technique used to efficiently manage database connections by reusing existing connections rather than creating new ones for each request. This can significantly improve the performance of database applications by reducing the overhead of establishing new connections.

#### Implementing Connection Pooling in PyODBC
PyODBC does not have built-in support for connection pooling, but it can be implemented using third-party libraries such as `pypyodbc`, `pyodbc-pool`, or `SQLAlchemy`.

Here's a basic example using `pyodbc-pool`:

```python
from pyodbc_pool import ConnectionPool

# Set up connection parameters
pool = ConnectionPool(
    initial_size=5,
    max_overflow=10,
    pool_timeout=30,
    echo=True,
    **connection_kwargs
)

# Get a connection from the pool
conn = pool.connect()

# Perform database operations
cursor = conn.cursor()
cursor.execute("SELECT * FROM your_table")
result = cursor.fetchall()

# Release the connection back to the pool
cursor.close()
pool.putconn(conn)
```

Replace `connection_kwargs` with your actual connection parameters such as DSN, UID, PWD, etc.

### 3. Working with NoSQL Databases

#### What are NoSQL Databases?
NoSQL databases are non-relational databases that provide flexible schema design and horizontal scalability. Examples include MongoDB, Couchbase, and Cassandra.

#### Using PyODBC with NoSQL Databases
While PyODBC is primarily designed for relational databases, you can still use it to connect to NoSQL databases that have ODBC drivers available. Here's a basic example using PyODBC with MongoDB:

```python
import pyodbc

# Establish a connection to MongoDB using ODBC driver
conn = pyodbc.connect('DSN=mongodb_odbc_dsn;UID=username;PWD=password')

# Create a cursor object
cursor = conn.cursor()

# Example of querying MongoDB using SQL syntax (requires ODBC SQL support)
cursor.execute("SELECT * FROM your_mongodb_collection")

# Fetch the result if needed
result = cursor.fetchall()

# Close the cursor and connection
cursor.close()
conn.close()
```

Replace `mongodb_odbc_dsn`, `username`, `password`, and `your_mongodb_collection` with your actual DSN, credentials, and collection name.
