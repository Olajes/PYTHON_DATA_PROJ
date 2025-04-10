# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the 5 skills for these top 3 rles. This query highlights the most popular job_titles and their skills, showing which skills I should pay attention to dependiing on the role I'm targeting.

View my notebook with detailed steps here:
[2_skills_Demand.ipynb](3_Project/2_skills_Demand.ipynb)

### Visualize Data
```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')

for i, job_title in enumerate (job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    #df_plot.plot(kind='barh', x='job_skills', y='skill_percent', ax=ax[i], title = job_title)
    sns.barplot(data = df_plot, x= 'skill_percent', y='job_skills', ax=ax[i], hue= 'skill_count', palette = 'dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 78)

    for n,v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1,n,f'{v:.0f}%', va='center')
    
    
    if i != len(job_titles) -1:
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize= 15)
fig.tight_layout(h_pad= 0.5)
plt.show()
```

## Results

![Visualization of Top Skills For Data Nerds]
("C:\Users\user\Desktop\STEVE HTML\PYTHON_DATA_PROJECT\3_Project\skill_demand_all_data_role.png")


## Insight

- Python is a versatile skill, highly demanded across all three roles,but most prominently for Data Scientists(72%) and Data Engineers (65%).
- SQL is the most requested skill for Data Analyst and Data Scientists, with it in over half the Job Posting for both roles. For Data Engineers, Python is the most sought -after skill, appearing in 68% of job postings.
- Data Enginners requires more specialized technical skills(AWS, Azure, Spark) compared to Data Analyst and Data Scientist who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).


## 2. How are in-demand skills trending for Data Analyst?

### Visualize Data
```python
df_plot = df_DA_US_percent.iloc[:, :5]

sns.lineplot(data= df_plot, dashes= False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analyst in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()


from matplotlib.ticker import PercentFormatter
ax= plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.2, df_plot.iloc[-1,i], df_plot.columns[i])

```
## Results

![Visualization of Trending Top Skills for Data Analyst]
("C:\Users\user\Desktop\STEVE HTML\PYTHON_DATA_PROJECT\3_Project\Skill_Trend.png")
*Bar graph visualizing the trending top skills data analyst in 2024.*

### Insight
- SQL remains the most consistency demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel experienced a significant increase in demand starting around september, surpassing both Python anad Tableau by end the year.
- Both python and Tableau show relatively satble demand throughtout the year with some Fluctions but remain essential skills for data anlayst.. PowerBI, while less demanded compared to the Tableau.


## 2. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds
```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

sns.set_theme(style='ticks')
#this is all the same

plt.title('Salary Distribution in Dollars')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0,600000)
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}k')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```python

## Results

![Visualization of Salary Analysis for Data Nerds]
("C:\Users\user\Desktop\STEVE HTML\PYTHON_DATA_PROJECT\3_Project\images\Salary_Analysis.png")
*Box plot visualizing the salary distributions for the top 6 data job titles.*


### Insight
- There is a significant variation in salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to $600k, indicting the high value placed on the advanced data skills and experienced in the Industry.

- Senior Data Enginner and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting the exceptional skills or circustances can lead to high pay in these roles. In Contrast, Data Analyst roles demonstrate more consisitency in salary, with fewer outliers.

- The Median salaries increase with the seniority and specialization of the roles. Senior roles ( Senior Data Sientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsiblities increase.








