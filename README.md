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

<h3>Q11 Count the number of unique street names for each postal code in the business dataset. Use only the first word of the street name, case insensitive (e.g., "FOLSOM" and "Folsom" are the same). If the structure is reversed (e.g., "Pier 39" and "39 Pier"), count them as the same street. Output the results with postal codes, ordered by the number of streets (descending) and postal code (ascending).</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>sf_restaurant_health_violations</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
s = sf_restaurant_health_violations
rect_st = []

for i in s.index:
    sent = s.business_address[i].lower()
  
    #take index instantly after split
    sent = sent.split()
    res = []
    for i in range(len(sent)):
        if sent[0].isdigit() == True:
            if sent[i] == sent[0]:
                pass
            # using any for making code shortly
            elif any(sub in sent[i] for sub in ['st', 'ave', 'plaza', 'bl', 'pl']):
                break
            else:
                res.append(sent[i])
        else:
            if sent[i].isdigit() == True:
                break
            else:
                res.append(sent[i])
            
    rect_st.append(' '.join(res))
    
    
#creating new column with an array
s['new_sreet'] = rect_st

res = s[['business_postal_code', 'new_sreet']]

#.nunique() is the same like select distinct
res.groupby(['business_postal_code']).nunique().sort_values(by = ['new_sreet'], ascending = False).dropna().reset_index()
</code></pre>

<h3>Q12 Find the review_text that received the highest number of  cool votes.
Output the business name along with the review text with the highest number of cool votes.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>yelp_reviews</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
y = yelp_reviews

res = y[['business_name', 'review_text']].where(y['cool'] == y['cool'].max()).dropna()
</code></pre>

<h3>Q13 Find the average total compensation based on employee titles and gender. Total compensation is calculated by adding both the salary and bonus of each employee. However, not every employee receives a bonus so disregard employees without bonuses in your calculation. Employee can receive more than one bonus.
Output the employee title, gender (i.e., sex), along with the average total compensation.</h3>
<h3>💾 DataFrames Used:</h3>
<ul>
  <li><code>sf_employee</code></li>
  <li><code>sf_bonus</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
e = sf_employee
b = sf_bonus.groupby(['worker_ref_id']).sum()

j = pd.merge(e, b, left_on = 'id', right_on = 'worker_ref_id', how = 'inner').sort_values(by = 'employee_title', ascending = True)

j['total_comp'] = j['salary'] + j['bonus']
j[['employee_title', 'sex', 'total_comp']].groupby(['employee_title', 'sex']).mean().reset_index()
</code></pre>

<h3>Q14 Identify customers who did not place an order between 2019-02-01 and 2019-03-01.</h3>
<h3>💾 DataFrames Used:</h3>
<ul>
  <li><code>customers</code></li>
  <li><code>orders</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
c = customers
o = orders

gather = pd.merge(c, o, left_on = 'id', right_on = 'cust_id', how = 'left')

last_check = []
first_name = []
res1 = []
for x in gather.index:
    check = gather['order_date'][x]
    
    #cheking for NaN type
    if pd.isnull(check) or (check < pd.to_datetime('2019-02-01') or check > pd.to_datetime('2019-03-01')):
        first_name.append(gather['first_name'][x])
    else:
        last_check.append(gather['first_name'][x])
       
for i in first_name:
    if i not in last_check:
        res1.append(i)
res = {
    'first_name' : res1
}

res = pd.DataFrame(res)
res.drop_duplicates()
</code></pre>

<h3>Q15 Output the number of survivors and non-survivors by each class.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>titanic</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
t = titanic

t_f = t[['survived', 'pclass']].where(t['pclass'] == 1).dropna().groupby(['survived']).count().reset_index()
t_s = t[['survived', 'pclass']].where(t['pclass'] == 2).dropna().groupby(['survived']).count().reset_index()
t_t = t[['survived', 'pclass']].where(t['pclass'] == 3).dropna().groupby(['survived']).count().reset_index()

res = pd.merge(t_f, t_s, left_on = 'survived', right_on = 'survived', how = 'inner')
res1 = pd.merge(res, t_t, left_on = 'survived', right_on = 'survived', how = 'inner')

res1.rename(columns={'pclass_x': 'first_class', 'pclass_y': 'second_classs', 'pclass': 'third_class'})
</code></pre>

<h3>Q16 Which user flagged the most distinct videos that ended up approved by YouTube? Output, in one column, their full name or names in case of a tie. In the user's full name, include a space between the first and the last name.</h3>
<h3>💾 DataFrames Used:</h3>
<ul>
  <li><code>user_flags</code></li>
  <li><code>flag_review</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
u = user_flags
f = flag_review
  
m = pd.merge(u, f, left_on = 'flag_id', right_on = 'flag_id', how = 'left')
m['full_name'] = m['user_firstname'] + " " + m['user_lastname']
  
#conditions with and
m[(m['reviewed_by_yt'] == 1) & (m['reviewed_outcome'] == 'APPROVED')]
  
#select distinct
sub_res = m[['full_name', 'video_id']].dropna().drop_duplicates()
  
#grouping and sorting
res = sub_res.groupby(['full_name']).count().reset_index().sort_values(by = 'video_id', ascending = False)
  
#extract value from column 
n = res['video_id'].head(1).iloc[0]

res['full_name'].where(res['video_id'] == n).dropna()
</code></pre>

<h3>Q17 Find the number of times each word appears in the contents column across all rows in the google_file_store dataset. Output two columns: word and occurrences.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>google_file_store</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd
import re

# Start writing code
g = google_file_store
word = []
occurrences = []

for i in g.index:
    #if g.filename[i].startswith('draft'):
    #if 'draft' in (g.filename[i]):
        #for j in 
        arr = re.sub(r"[.,']", "", g.contents[i].lower()).split()
        for j in range(len(arr)):
            if arr[j] not in word:
                word.append(arr[j])
                occurrences.append(1)
            else:
                for o in range(len(word)):
                        #print(word[j])
                    if word[o] == arr[j]:
                        print(word[o], occurrences[o])
                        occurrences[o] += 1
                        
frame = {
    'words' : word,
    'occurrences' : occurrences
}
res = pd.DataFrame(frame)
res.sort_values(by = 'occurrences', ascending = True)
</code></pre>

<h3>Q18 Calculate the net change in the number of products launched by companies in 2020 compared to 2019. Your output should include the company names and the net difference.
(Net difference = Number of products launched in 2020 - The number launched in 2019.)</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>car_launches</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
c = car_launches
c_19 = c[['company_name', 'product_name']].where(c['year'] == 2019).groupby(['company_name']).count().reset_index().sort_values(by = ['company_name'], ascending = True)
c_20 = c[['company_name', 'product_name']].where(c['year'] == 2020).groupby(['company_name']).count().reset_index().sort_values(by = ['company_name'], ascending = True)
  
res = pd.merge(c_19, c_20, left_on = 'company_name', right_on = 'company_name', how = 'inner')
res['difference'] = res['product_name_y'] - res['product_name_x']
  
res[['company_name', 'difference']]
</code></pre>

<h3>Q19 Find the top 10 ranked songs in 2010. Output the rank, group name, and song name, but do not show the same song twice. Sort the result based on the rank in ascending order.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>billboard_top_100_year_end</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
b = billboard_top_100_year_end
res = b[(b['year'] == 2010)].sort_values(by = ['year_rank'], ascending = True)
r = res[['group_name', 'song_name']]
r = r.drop_duplicates().head(10)
  
r['rank'] = range(1, len(r) + 1)
r[['rank', 'group_name','song_name']].head(10)
</code></pre>

<h3>Q20 Calculate the total revenue from each customer in March 2019. Include only customers who were active in March 2019. An active user is a customer who made at least one transaction in March 2019.
Output the revenue along with the customer id and sort the results based on the revenue in descending order.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>orders</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
o = orders#.head()
o['month_'] =  o['order_date'].dt.month
w = o.where(o['month_'] == 3).dropna(how = 'all')
w = w[['cust_id', 'total_order_cost']].groupby('cust_id').sum('total_order_cost').sort_values(by = 'total_order_cost', ascending = False).reset_index()
</code></pre>
<h2 id ='hard'>🎯 Difficulty Level - Hard</h2>

<h3>Q21 Select the most popular client_id based on the number of users who individually have at least 50% of their events from the following list: 'video call received', 'video call sent', 'voice call received', 'voice call sent'.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>fact_events</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
f = fact_events
c = f.where(f['event_type'].isin(['video call received', 'video call sent', 'voice call received', 'voice call sent'])).dropna()
n = c.count()[0]
c = c[['client_id', 'event_type']].groupby(['client_id']).count().reset_index()
res = []
for i in c.index:
    if n / 2 <= c['event_type'][i]:
        res.append(c['client_id'][i])

result = {
    'client_id': res
}
pd.DataFrame(result)
</code></pre>

<h3>Q22 Determine the minimum, average, and maximum rental prices for each popularity-rating bucket. A popularity-rating bucket should be assigned to every record based on its number_of_reviews. 
Output host popularity rating and their minimum, average and maximum rental prices. Order the solution by the minimum price.</h3>
<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>airbnb_host_searches</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
a = airbnb_host_searches
popularity = []
for i in a.index:
    if a['number_of_reviews'][i] == 0:
        popularity.append('New')
    elif a['number_of_reviews'][i] in range(1, 6):
        popularity.append('Rising')
    elif a['number_of_reviews'][i] in range(6, 16):
        popularity.append('Trending Up')
    elif a['number_of_reviews'][i] in range(16, 41):
        popularity.append('Popular')
    elif a['number_of_reviews'][i] > 40:
        popularity.append('Hot')
    else:
        popularity.append('')
a['popularity'] = popularity
a.head()
min_ = a[['popularity', 'price']].groupby('popularity').min().reset_index()
max_ = a[['popularity', 'price']].groupby('popularity').max().reset_index()
avg_ = a[['popularity', 'price']].groupby('popularity').mean().reset_index()

pre_res = pd.merge(min_, avg_, left_on = 'popularity', right_on = 'popularity', how = 'inner')
res = pd.merge(pre_res, max_, left_on = 'popularity', right_on = 'popularity', how = 'inner')
res.sort_values(by = 'price_x', ascending = True)
</code></pre>

<h3>Q23 You're given a dataset of searches for properties on Airbnb. For simplicity, let's say that each search result (i.e., each row) represents a unique host. Find the city with the most amenities across all their host's properties. Output the name of the city.</h3>
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

count_amenities = []

for i in a.index:
    count = 0
    amenities = []
    #print(type(a['amenities'][i].split(',')))
    for j in a['amenities'][i].split(','):
        if j not in amenities:
            count += 1
    count_amenities.append(count)
a['count_amenities'] = count_amenities
a = a[['count_amenities', 'city']].sort_values(by = 'count_amenities', ascending = False)    
a['city'].head(1)
</code></pre>

<h3>Q24 Find the number of times the exact words bull and bear appear in the contents column.
Count all occurrences, even if they appear multiple times within the same row. Matches should be case-insensitive and only count exact words, that is, exclude substrings like bullish or bearing
Output the word (bull or bear) and the corresponding number of occurrences.</h3>

<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>google_file_store</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
g = google_file_store
words = ['bull', 'bear']
res = [0, 0]
for i in g.index:
    for j in g['contents'][i].split(' '):
        if j == 'bull':
            res[0] += 1
        elif j == 'bear':
            res[1] += 1
d = {
    'word' : words,
    'netry' : res
}
pd.DataFrame(d)
</code></pre>

<h3>Q25 Find the top 5 states with the most 5 star businesses.</h3>

<h3>💾 DataFrame Used:</h3>
<ul>
  <li><code>yelp_business</code></li>
</ul>

<h3>🧪 Solution (Using <code>pandas</code>):</h3>

<pre><code class="language-python">
# Import your libraries
import pandas as pd

# Start writing code
y = yelp_business
state = y['state'].drop_duplicates()
res = pd.DataFrame()
  
for i in state.index:
    res = pd.concat([res, y[(y['state'] == state[i]) & (y['stars'] == 5)].groupby('state').count().reset_index()], ignore_index = True)
  
res = res[['state', 'business_id']]#.sort_values(by = 'business_id', ascending = False).head(5)
res['rank'] = res['business_id'].rank(method = 'dense', ascending = False)
  
res[['state', 'business_id']].where(res['rank'] <= 5).dropna().sort_values(by = ['business_id', 'state'], ascending = False)
</code></pre>
