# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which ones were the most popular and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills showinf which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here: [name of the file](path of the file)


sns.set_theme(style='ticks')

fig, ax = plt.subplots(len(job_titles),1)

```python
for i, job_title in enumerate(job_titles): 
    df_plot = df_skill_perc[df_skill_perc['job_title_short'] == job_title].sort_values(by='skill_perc', ascending=True).tail(5)
    sns.barplot(data=df_plot, x='skill_perc', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].invert_yaxis()
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_title(job_title)
    ax[i].set_xlabel('')
    ax[i].set_xlim(0,80)    

    for n, v in enumerate(df_plot['skill_perc']):
        ax[i].text(v+3, n, f'{v:.0f}%', va='center') 

    if i != len(job_titles)-1:
        ax[i].set_xticks([])


fig.suptitle('Likelihood skills Requested in US job Postings', fontsize=15)

fig.tight_layout()
plt.show()
```

 - Python is a versatile skill, highly demanded accreoss all three roles but most prominently for Data Scientist (72%) and Data Engineers (65%).
 - SQL is the most requested skill for Data Analysts and Data Scientists with it in over half of the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of the job postings.
 - Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).

