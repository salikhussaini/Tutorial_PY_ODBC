**Python Tutorial: Advanced Data Retrieval Techniques**

In this tutorial, we'll explore advanced data retrieval techniques using PyODBC, focusing on fetching large datasets efficiently, optimizing memory usage by fetching data in chunks, and effectively utilizing the `fetchmany()` and `fetchall()` methods.

**1. Fetching Large Datasets Efficiently:**

When dealing with large datasets, fetching all the data at once can lead to memory issues. To address this, we can fetch data in chunks using cursors. Let's see how:

```python
import pyodbc

# Establish a connection to the database
connection = pyodbc.connect("DSN=YourDataSourceName;UID=YourUsername;PWD=YourPassword")

# Create a cursor
cursor = connection.cursor()

# Execute a query
cursor.execute("SELECT * FROM large_table")

# Fetch data in chunks
chunk_size = 1000
while True:
    rows = cursor.fetchmany(chunk_size)
    if not rows:
        break
    # Process the fetched data (e.g., perform calculations, store in a list, etc.)
    for row in rows:
        print(row)

# Close the cursor and connection
cursor.close()
connection.close()
```

**2. Fetching Data in Chunks to Optimize Memory Usage:**

Fetching data in chunks allows us to process a manageable amount of data at a time, reducing memory consumption. We can adjust the `chunk_size` according to our system's memory capacity.

**3. Utilizing `fetchmany()` and `fetchall()` Effectively:**

The `fetchmany()` method retrieves the next set of rows up to the specified size, while `fetchall()` fetches all remaining rows. Let's see how to use them:

```python
# Fetching data using fetchmany()
cursor.execute("SELECT * FROM large_table")
rows = cursor.fetchmany(1000)  # Fetches 1000 rows at a time

# Fetching all remaining rows using fetchall()
cursor.execute("SELECT * FROM large_table")
rows = cursor.fetchall()  # Fetches all remaining rows
```

**4. Hands-on Exercises on Fetching Large Datasets:**

Exercise 1: Fetch data from a large table in your database in chunks of 500 rows each and calculate the average of a numeric column.

Exercise 2: Fetch all rows from a large table and store them in a pandas DataFrame in batches of 2000 rows each.

---

**Python Tutorial: Data Manipulation and Transactions**

In this tutorial, we'll cover data manipulation techniques and transaction management in PyODBC, including performing bulk data inserts, updates, and deletes, handling errors, and rollbacks.

**1. Performing Bulk Data Inserts, Updates, and Deletes:**

PyODBC allows us to execute SQL statements for bulk data operations efficiently. Here's how:

```python
# Bulk insert
data = [(1, 'John'), (2, 'Jane'), (3, 'Doe')]
cursor.executemany("INSERT INTO users (id, name) VALUES (?, ?)", data)

# Bulk update
cursor.executemany("UPDATE users SET name = ? WHERE id = ?", [("Jane Doe", 2), ("John Doe", 3)])

# Bulk delete
ids_to_delete = [4, 5, 6]
cursor.executemany("DELETE FROM users WHERE id = ?", [(id,) for id in ids_to_delete])
```

**2. Understanding Transaction Management in PyODBC:**

Transactions allow us to group multiple SQL operations into a single unit of work, ensuring data integrity. Here's how to use transactions in PyODBC:

```python
# Begin a transaction
connection.autocommit = False

# Execute SQL statements within the transaction
try:
    cursor.execute("INSERT INTO table1 (column1) VALUES ('value1')")
    cursor.execute("UPDATE table2 SET column2 = 'new_value' WHERE condition")
    # Commit the transaction if all statements are successful
    connection.commit()
except:
    # Rollback the transaction in case of any error
    connection.rollback()
```

**3. Handling Errors and Rollbacks in Transactions:**

It's crucial to handle errors gracefully and rollback the transaction if any operation fails to maintain data consistency.

**4. Hands-on Exercises on Data Manipulation and Transactions:**

Exercise 1: Perform a bulk update on a table in your database, setting a new value for a specific column based on a condition.

Exercise 2: Implement a transaction that inserts records into two related tables. Roll back the transaction if the insertion into the second table fails.

---
