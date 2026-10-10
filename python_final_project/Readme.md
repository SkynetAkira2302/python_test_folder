# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which ones were the most popular and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills showinf which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here: [name of the file](path of the file)

```python
sns.set_theme(style='ticks')

fig, ax = plt.subplots(len(job_titles),1)


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

# 2. How are in demand skills trending for Data Analysts?

To find the most demanded skills trend troughout the year, first was created a copy of the dataset and filtered with "Data Analyst" job postings only, this help us to identify for data Analyst only the skills that repeat constantly in the job postings, the I created a total row temporally to get the top skills divided by month for plotting purposes. After having the total, the data was filtered to show only the top 5 skills plotted with the following code: 

```python
df_plot = df_DA_US_perc.iloc[:,:5]

sns.lineplot(df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()
plt.title('Top 5 skills trend monthly')
plt.xlabel('2023')
plt.ylabel('Likelihood in Job Posting')
plt.legend().remove()
#required module to turn axis on percentage
from matplotlib.ticker import PercentFormatter
ax =plt.gca()
#command line to change y axis to percentage format, since requires to confirm decimals otherwise will show code line
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))
#for loop to name the variables ploted in this case the skills 
for i in range(5):
    plt.text(11.2, df_plot.iloc[-1,i], df_plot.columns[i])
```

With this excercise I confirmed the following: 
- With multiple libraries on python such as pandas, matplotlib and seaborn can create charts that are customizable as can be done in excel or Power BI. 
- The level of customization can be really in-deep based on the knowledge of the libraries, since can customiza from color, type of line, remove frame or even add more visual details.
- Even when a chart can be done with pandas or matplotlib, for customization the one that provides more options is definetely seaborn. Since provide a customization as easy as one additional line of code, something that can be achieved as well with matplotlib but with more lines. My conclusion is that code related its better seaborn since provide a "friendly" customization compared to other libraries.
