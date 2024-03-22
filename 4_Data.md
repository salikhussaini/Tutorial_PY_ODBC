## Python Tutorial: Data Manipulation and Analysis

### Module 4: Data Manipulation and Analysis

In this module, we'll cover the essential concepts of data manipulation and analysis using PyODBC for database interactions and Python libraries like Pandas for data analysis.

### Data Manipulation

Data manipulation involves operations such as inserting, updating, and deleting data in a database using PyODBC.

#### 1. Inserting Data

To insert data into a database using PyODBC, you'll typically follow these steps:

```python
import pyodbc

# Establish a connection to the database
conn = pyodbc.connect('DSN=your_dsn;UID=username;PWD=password')

# Create a cursor object to execute SQL queries
cursor = conn.cursor()

# Define the SQL query to insert data
sql_insert = "INSERT INTO your_table (column1, column2, column3) VALUES (?, ?, ?)"

# Execute the SQL query with data
data = (value1, value2, value3)
cursor.execute(sql_insert, data)

# Commit the transaction
conn.commit()

# Close the cursor and connection
cursor.close()
conn.close()
```

#### 2. Updating Data

To update existing data in a database using PyODBC, you can use the following approach:

```python
# Establish a connection and create a cursor object (same as above)

# Define the SQL query to update data
sql_update = "UPDATE your_table SET column1 = ? WHERE condition"

# Execute the SQL query with data
new_value = "new_value"
cursor.execute(sql_update, new_value)

# Commit the transaction
conn.commit()

# Close the cursor and connection
cursor.close()
conn.close()
```

#### 3. Deleting Data

To delete data from a database using PyODBC, you can use the following method:

```python
# Establish a connection and create a cursor object (same as above)

# Define the SQL query to delete data
sql_delete = "DELETE FROM your_table WHERE condition"

# Execute the SQL query
cursor.execute(sql_delete)

# Commit the transaction
conn.commit()

# Close the cursor and connection
cursor.close()
conn.close()
```

### Data Analysis

Data analysis involves extracting insights and patterns from data retrieved from databases. We'll explore techniques for data analysis using Python libraries like Pandas.

#### 1. Installing Pandas

Before using Pandas, you need to install it. You can do this using pip:

```bash
pip install pandas
```

#### 2. Importing Pandas

```python
import pandas as pd
```

#### 3. Analyzing Data with Pandas

Once you have retrieved data from the database using PyODBC, you can analyze it using Pandas. Here's a simple example:

```python
# Assume 'data' is retrieved from the database using PyODBC
data = [...]

# Create a DataFrame from the retrieved data
df = pd.DataFrame(data, columns=['column1', 'column2', 'column3'])

# Perform analysis on the DataFrame
# Example: Calculate descriptive statistics
statistics = df.describe()

# Example: Filter data based on conditions
filtered_data = df[df['column1'] > 50]

# Example: Group data and perform aggregation
grouped_data = df.groupby('column2').agg({'column3': 'sum'})

# Example: Visualize data
df.plot(kind='scatter', x='column1', y='column2')

# More advanced analysis and visualization techniques can be applied as needed.
```
