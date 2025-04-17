#Task7

Task 7 Summary: Basic Sales Summary using SQLite and Python

In this task, I used SQLite with Python in a Jupyter Notebook environment to perform basic data analysis on sales data. Below is a step-by-step explanation of the operations I performed:

1. Database Connection: I established a connection to a local SQLite database named sales_data.db using the sqlite3 module:

conn = sqlite3.connect("sales_data.db")

This allowed me to interact with the database and execute SQL commands from within Python.


2. Table Creation: I ensured the existence of a sales table by running a CREATE TABLE IF NOT EXISTS SQL command. This table includes fields for product name, quantity sold, and price:

cursor.execute('''
CREATE TABLE IF NOT EXISTS sales (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    product TEXT NOT NULL,
    quantity INTEGER NOT NULL,
    price REAL NOT NULL
)
''')


3. Data Insertion: I inserted a set of sample sales records into the sales table to simulate real sales data. This step was done using the executemany() function:

sample_data = [
    ('Apple', 10, 1.5),
    ('Banana', 20, 0.5),
    ('Orange', 15, 1.0),
    ('Apple', 5, 1.5),
    ('Banana', 10, 0.5),
    ('Orange', 10, 1.0),
]
cursor.executemany("INSERT INTO sales (product, quantity, price) VALUES (?, ?, ?)", sample_data)
conn.commit()


4. Running SQL Query for Aggregation: I wrote and executed a SQL query to retrieve the total quantity sold and total revenue for each product. The query was defined as a multi-line string in Python:

query = '''
SELECT product, 
       SUM(quantity) AS total_qty, 
       SUM(quantity * price) AS revenue 
FROM sales 
GROUP BY product
'''

I then used pandas.read_sql_query() to execute the query and load the result into a DataFrame:

df = pd.read_sql_query(query, conn)


5. Displaying the Results: The resulting summary was printed using print(df) to show total quantities and revenue per product.


6. Visualization with Matplotlib: To better understand the revenue distribution, I plotted a bar chart using matplotlib:

df.plot(kind='bar', x='product', y='revenue', legend=False, color='skyblue')
plt.title('Revenue by Product')
plt.xlabel('Product')
plt.ylabel('Revenue')
plt.tight_layout()
plt.savefig("sales_chart.png")
plt.show()


7. Closing the Connection: Finally, I closed the database connection to release system resources:

conn.close()




---

This task helped me practice how to:

Create and manipulate a SQLite database

Write and run SQL queries inside Python

Use pandas for data handling

Visualize simple summaries using matplotlib

