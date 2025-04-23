Basic Sales Summary from a Tiny SQLite Database using Python
This project demonstrates how to connect a simple SQLite database to Python, run SQL queries to fetch sales data, and visualize basic sales summary using pandas and matplotlib.

📌 Objective
The goal of this project is to:

Use SQL within Python to query basic sales data (e.g. total quantity sold, total revenue).

Display the queried results using print statements and a basic bar chart.

🛠 Tools & Libraries
Python 3.x (Built-in SQLite support)

SQLite (No need for external installation)

pandas (For data handling)

matplotlib (For data visualization)

Jupyter Notebook or any Python script editor (VS Code, PyCharm, etc.)

📋 Dataset
A single SQLite table named sales is used to store sample sales data. The table contains the following columns:

id: Primary key (integer)

product: Product name (text)

quantity: Quantity of product sold (integer)

price: Price per unit of the product (real)

Example data:


id	product	quantity	price
1	Product A	10	15.5
2	Product B	5	23.0
3	Product C	8	30.0
4	Product D	15	12.0
🚀 How to Run the Project
Step 1: Clone the Repository
To start using the project, clone the repository to your local machine by running the following command in your terminal:

bash
Copy
Edit
git clone https://github.com/madhanarasan/Task-7
Step 2: Set up SQLite Database
The SQLite database will be created automatically in the script. If needed, you can also initialize a fresh database with the provided schema and sample data.

Here is an example script to create the database and insert some sample data:

python
Copy
Edit
import sqlite3

# Connect to SQLite database (or create it)
conn = sqlite3.connect('sales_data.db')
cursor = conn.cursor()

# Create sales table
cursor.execute('''
CREATE TABLE IF NOT EXISTS sales (
    id INTEGER PRIMARY KEY,
    product TEXT,
    quantity INTEGER,
    price REAL
)
''')

# Insert some sample data
cursor.executemany('''
INSERT INTO sales (product, quantity, price) VALUES (?, ?, ?)
''', [
    ('Product A', 10, 15.5),
    ('Product B', 5, 23.0),
    ('Product C', 8, 30.0),
    ('Product D', 15, 12.0)
])

conn.commit()
conn.close()
Step 3: Query the Database
After setting up the database, run the Python script to query the sales data from the database. Here’s a simple query to fetch the total quantity sold and total revenue for each product:

python
Copy
Edit
import sqlite3
import pandas as pd

# Connect to SQLite database
conn = sqlite3.connect('sales_data.db')

# Query to get total quantity and total revenue for each product
query = '''
SELECT product, SUM(quantity) as total_quantity, SUM(quantity * price) as total_revenue
FROM sales
GROUP BY product
'''

# Load data into a pandas DataFrame
sales_data = pd.read_sql(query, conn)

# Close the database connection
conn.close()

# Display the data
print(sales_data)
Step 4: Visualize the Data
After querying the data, use matplotlib to visualize the sales data in a simple bar chart. Here’s how you can plot the total revenue for each product:

python
Copy
Edit
import matplotlib.pyplot as plt

# Plot a bar chart for total revenue by product
sales_data.plot(kind='bar', x='product', y='total_revenue', color='skyblue', legend=False)

# Set labels and title
plt.xlabel('Product')
plt.ylabel('Total Revenue ($)')
plt.title('Total Revenue by Product')

# Show the plot
plt.show()
Expected Outputs
1. Printed Sales Summary
The printed output will show a tabular representation of the total quantity sold and the total revenue for each product. Example output:

mathematica
Copy
Edit
    product  total_quantity  total_revenue
0  Product A              10            155.0
1  Product B               5            115.0
2  Product C               8            240.0
3  Product D              15            180.0
2. Bar Chart
A bar chart will display the total revenue for each product. The x-axis will show the product names, and the y-axis will represent the total revenue in dollars.

🔧 Additional Features
You can modify the project to include additional features:

More Complex Queries: Add queries for average price per product or total sales per day.

Styling the Chart: Customize the chart with different colors, fonts, or other visual elements.

Dynamic Input: Accept dynamic inputs like date ranges or specific products to generate filtered reports.

💡 Requirements
pandas: To install pandas, run the following command:

bash
Copy
Edit
pip install pandas
matplotlib: To install matplotlib, run:

bash
Copy
Edit
