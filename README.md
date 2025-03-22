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




















