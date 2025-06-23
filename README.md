# Pandas_solving_tasks_stratascratch
This repository contains solutions to Python data manipulation tasks from StrataScratch using the pandas library. Each notebook is focused on solving real-world data analytics and data science problems, commonly asked in technical interviews and assessments.
- [Easy](/#easy)
- [Medium](#medium)
- [Hard](#hard)
<p>📚 Contents:
📊 Data Cleaning – Handling missing values, duplicates, and formatting.

📈 Data Transformation – Grouping, filtering, aggregations, and joins using pandas.

🧠 Logic & Analysis – Business logic applied through pandas for insights and KPIs.

✅ Interview-style Challenges – Solutions to popular data science questions using pandas.</p>
<h2 id ='easy'>🎯 Difficulty Level - Easy</h2>
<h3>Q1 Find all posts which were reacted to with a heart. For such posts output all columns from facebook_posts table.</h3>
<h3>💾 DataFrames Used:</h3>
<ul>
  <li><code>facebook_reactions</code></li>
  <li><code>facebook_posts</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
import pandas as pd

# Assigning the dataframes
f_r = facebook_reactions
f_p = facebook_posts

# Joining the reactions and posts on post_id
j = pd.merge(f_r, f_p, left_on='post_id', right_on='post_id', how='left')

# Filtering for 'heart' reactions only
j = j.where(j['reaction'] == 'heart').dropna()

# Selecting relevant columns and removing duplicates
res = j[['post_id', 'poster_x', 'post_text', 'post_keywords', 'post_date']].drop_duplicates()
</code></pre>
<h3>Q2 Calculates the difference between the highest salaries in the marketing and engineering departments. Output just the absolute difference in salaries.</h3>
<h3>💾 DataFrames Used:</h3>
<ul>
  <li><code>db_employee</code></li>
  <li><code>db_dept</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
e = db_employee
d = db_dept
  
# merge two tables with each other by lest join
j = pd.merge(e, d, left_on = 'department_id', right_on = 'id', how = 'left')
  
# extract the biggest salary from departments
eng = j.where(j['department'] == 'engineering').sort_values(by = 'salary', ascending = False).drop_duplicates().head(1)
mar = j.where(j['department'] == 'marketing').sort_values(by = 'salary', ascending = False).drop_duplicates().head(1)
  
#select index in the tables
eng = eng.reset_index(drop=True)
mar = mar.reset_index(drop=True)
  
#creating result with subtraced salary
res['salary_difference'] = mar['salary'] - eng['salary']
</code></pre>

<h3>Q3 We have a table with employees and their salaries, however, some of the records are old and contain outdated salary information. Find the current salary of each employee assuming that salaries increase each year. Output their id, first name, last name, department ID, and current salary. Order your list by employee ID in ascending order.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>ms_employee_salary</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
t = ms_employee_salary

t[['id', 'first_name', 'last_name', 'department_id', 'salary']] = t.groupby(['id', 'first_name', 'last_name', 'department_id']).max().reset_index().head(100)
</code></pre>

<h3>Q4 Compare each employee's salary with the average salary of the corresponding department.
Output the department, first name, and salary of employees along with the average salary of that department.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>employee</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
e = employee#.head()
#sub_t = e[['department', 'first_name', 'salary']].groupby(['department', 'first_name', 'salary'])
t = e[['department', 'first_name', 'salary']].groupby(['department'])['salary'].mean().reset_index()
res = pd.merge(e, t, left_on = 'department', right_on = 'department', how = 'left')
res[['department', 'first_name', 'salary_x', 'salary_y']]
</code></pre>

<h3>Q5 Find order details made by Jill and Eva.
Consider the Jill and Eva as first names of customers.
Output the order date, details and cost along with the first name.
Order records based on the customer id in ascending order.</h3>
<h3>💾 DataFrames Used:</h3>
<ul>
  <li><code>customers</code></li>
  <li><code>orders</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
import pandas as pd
  
c = customers
o = orders
  
# Start writing code
c = c[['id', 'first_name']]#.where(c['first_name'].isin(['Eva', 'Jill'])).dropna().head()#('Eva', 'Jill')).head()
  
all_inform = pd.merge(c, o, how = 'right', left_on = 'id', right_on = 'cust_id')#.sort_values(by = c['id'], ascending = True)
  
r = all_inform[['id_x', 'first_name', 'order_date', 'order_details','total_order_cost']].where(all_inform['first_name'].isin(['Eva', 'Jill'])).dropna().sort_values(by = 'id_x', ascending = True)
r[['first_name', 'order_date', 'order_details','total_order_cost']].head(50)
</code></pre>

<h3>Q6 Find all Lyft drivers who earn either equal to or less than 30k USD or equal to or more than 70k USD.
Output all details related to retrieved records.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>lyft_drivers</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
l = lyft_drivers

part_1 = l.where(l['yearly_salary'] >= 70000)#.dropna()# or l['yearly_salary'] <= 30000)
part_2 = l.where(l['yearly_salary'] <= 30000)#.dropna()

res = pd.concat([part_1, part_2]).sort_values(by = 'index', ascending = True)#.dropna(how = 'all')
sorted_res = res.dropna(how = 'all')
</code></pre>

<h3>Q7 Find the number of employees working in the Admin department that joined in April or later.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>worker</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
w = worker
w['month'] =  w['joining_date'].dt.strftime('%m')
res = w[['worker_id']].where((w['department'] == 'Admin') & (w['month'] >= '04')).dropna().count()
</code></pre>

<h3>Q8 We have a table with employees and their salaries, however, some of the records are old and contain outdated salary information. Find the current salary of each employee assuming that salaries increase each year. Output their id, first name, last name, department ID, and current salary. Order your list by employee ID in ascending order.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>ms_employee_salary</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
t = ms_employee_salary

t[['id', 'first_name', 'last_name', 'department_id', 'salary']] = t.groupby(['id', 'first_name', 'last_name', 'department_id']).max().reset_index().head(100)
</code></pre>

<h3>Q9 Find the average number of bathrooms and bedrooms for each city’s property types. Output the result along with the city name and the property type.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>airbnb_search_details</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
a = airbnb_search_details
res = a[['city', 'property_type', 'bathrooms', 'bedrooms']].groupby(['city', 'property_type'])[['bathrooms', 'bedrooms']].mean().reset_index()
</code></pre>

<h3>Q10 Write a query that will calculate the number of shipments per month. The unique key for one shipment is a combination of shipment_id and sub_id. Output the year_month in format YYYY-MM and the number of shipments in that month.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>amazon_shipment</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
a = amazon_shipment
  
a['year_month'] = a['shipment_date'].dt.strftime('%Y-%m')
a[['sub_id','year_month']].groupby('year_month').count().reset_index().head()
</code></pre>

<h2 id ='medium'>🎯 Difficulty Level - Medium</h2>


