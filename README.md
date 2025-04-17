# The Analysis

## 1. What are the most demand skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here : [2_skills_demand.ipynb](3_Project\2_skills_count.ipynb)

### Visualize Data
```python
fig, ax = plt.subplots(len(job_titles),1)

for i , job_title in enumerate(job_titles):
    df_plot = df_skills_count[df_skills_count['job_title_short'] ==job_title].head(5)
    df_plot.plot(kind='barh', x='job_skills', y='skill_count',ax=ax[i], title=job_title)
    ax[i].invert_yaxis()
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)
    
fig.suptitle('Counts of Top Skills in Job Postings', fontsize=15)
fig.tight_layout(h_pad=0.5)
plt.show()

```

### Results

![Visualization of Top Skills for Data Nerds](3_Project\Images\skill_demand_all_data_roles.png)

### Insights

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).

- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.

- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).

## 2. How are in-demand skills trending for Data Analysts?

Visualize Data

```python
from matplotlib.ticker import PercentFormatter
sns.lineplot(data = df_plot, dashes = False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()
ax = plt.gca().ax.yaxis.set_major_formatter(PercentFormatter(decimals = 0))

plt.show()

```

## Results
![Trending Top Skills for Data Analyts in the US](3_Project\Images\skills_trend_DA.png)
- Line chart visualizing the trending top skills for data analysts in the US in 2023

### Insights

- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end of the year.
- Both Python and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts. Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.

## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds

#### Visualize Data 

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y= 'job_title_short', order =job_order)

ticks_x = plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```

#### Results

![Salary Distributions of Data Jobs in the US](3_Project\Images\salary_analysis.png)

### Insights

- There's a significant variation in salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to $600K, indicating the high value placed on advanced data skills and experience in the industry.

- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with fewer outliers.

- The median salaries increase with the seniority and specialization of the roles. Senior roles (Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.

# The Analysis
## 3. How well do jobs skills pay for Data Analysts
### Highest Paid & Most Demanaded Skills for Data Analysts
#### Visiaulization Data

```python

fig, ax = plt.subplots(2,1)
sns.set_theme(style="ticks")

sns.barplot(data = df_DA_top_pay, x = 'median', y= df_DA_top_pay.index, ax= ax[0], hue='median', palette ='dark:b_r')

sns.barplot(data = df_DA_skills, x = 'median', y= df_DA_skills.index, ax= ax[1], hue='median', palette ='light:b')

plt.show()
```

#### Results
In-Demand skills for Data analyts in the US

![The Highest Paid & Most In-Demand Skills for Data Analytics in the US](3_Project\Images\4_highest_paid_and_most_in_in_demand_skills_for_data_analyst_in_the_us.png)

- Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.

### Insights

- The top graph shows specialized technical skills like dplyr, Bitbucket, and Gitlab are associated with higher salaries, some reaching up to $200K, suggesting that advanced technical proficiency can increase earning potential.

- The bottom graph highlights that foundational skills like Excel, PowerPoint, and SQL are the most in-demand, even though they may not offer the highest salaries. This demonstrates the importance of these core skills for employability in data analysis roles.

- There's a clear distinction between the skills that are highest paid and those that are most in-demand. Data analysts aiming to maximize their career potential should consider developing a diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.


