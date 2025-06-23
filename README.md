# Pandas_solving_tasks_stratascratch
This repository contains solutions to Python data manipulation tasks from StrataScratch using the pandas library. Each notebook is focused on solving real-world data analytics and data science problems, commonly asked in technical interviews and assessments.
📚 Contents:
📊 Data Cleaning – Handling missing values, duplicates, and formatting.

📈 Data Transformation – Grouping, filtering, aggregations, and joins using pandas.

🧠 Logic & Analysis – Business logic applied through pandas for insights and KPIs.

✅ Interview-style Challenges – Solutions to popular data science questions using pandas.
<h2>🎯 Difficulty Level - Easy</h2>
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

