# 📘 Introduction

## Overview

Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for data analysts. 

The data sourced from Luke Barousse's Python Course which provides a foundation for my analysis, containing detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in data analytics. 

## The Questions

Below are the questions I want to answer in my project:
1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand and High Paying)

## Tools I used

For my deep dive inot the data analyst job market, I harnessed the power of several key tools: 

* **Python**: The backbone of my analysis, allowing me to analyse the data and find critical insights. I also used the following Python libraries: 
    * Pandas Library: This was used to analyse the data.
    * Matplotlib Library: To visualise the data.
    * Seaborn Library: To create more advanced visuals. 
* **Jupyter Notebooks**: The tool I used to run my python scripts which let me easily include my notes and analysis.
* **Git & GitHub**: Essential for version control and sharing my Python code and analysis, ensuring collaboration and 


# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles? 

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting. 

View my notebook with detailed steps here: [2_Skill_Demand.ipynb](3_Project/2_Skills_Count.ipynb)

### Visualise Data

```python

fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    
plt.show()
```

### Results

![Visualisation of Top Skills](3_Project/images/skill_demand_all_data_roles.png)


### Insights

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%). 
- SQL is the most requested still for Data Analysts and Data Engineers, with it in over half the job postings for both roles. For Data Engineers, SQL is the most sought-after skill, appearing in 68% of job postings. 
- Data Engineers require more specialised technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis toold (Excel, Tableau). 


## 2. How are in-demand skills trending for Data Analysts?

``` PYTHON

from matplotlib.ticker import PercentageFormatter

df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, palette='tab10)

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()
```

### Results

![Trending Top Kills for Data Analysts in the US](3_Project/images/skill_trend_DA.png)

*Bar graph visualising the trending top skills for data analyssts in the US in 2023.*

### Insights:
- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand. 
- Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end of the year. 
- Both Python and Tableau show relatiively stable demand throughout the year with some fluctuations but remain essential skillls for data analysts. Power BI, while less demanded compared to the others, shows a slight upward trend towards the years end. 


## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Positions

#### Visualise Data

``` python

sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```

#### Results
![Salary Distribution of Data Jobs in the US](3_Project/images/Salary_Dis_US.png)
*Box plot visualising the salary distributions for the top 6 data job titles.*

- There's a significant variation in salary ranges across different job titles. Data Scientist positions tend to have the highest salary potential, with up to $600K, indicating the high value placed on advanced data skills and experience in the industry.

- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with fewer outliers.

- The median salaries increase with the seniority and specialisation of the roles. Senior roles (Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase. 


### Highest Paid & Most Demanded Skills for Data Analysts

```python

fig, ax = plt.subplots(2,1)

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()

```

Here's the breakdown of the highest-paid and most in-demand skills for data analysts in the US:

![The Highest Paid & Most In-Demand Skills for Data Analysts in the US](3_Project/images/Top10_skills_DA.png)
*Two seperate bar graphs visualising the highest paid and most in-demand skills for data analysts in the US.*

#### Insights:

- The top graphs shows specialised technical skills like `dply`', `Bitbucket`, and `Gitlab` are associated with higher salaries, some reaching up to $200K, suggesting that advanced technical proficiency can increase earning potential.

- The bottom graph highlights that foundational skills like `Excel`, `Powerpoint` and `SQL` are the most in-demand, even though they may not offer the hightest salaries. This demonstrates the importance of these core skills for employability in data analysis roles.

- There's a clear distinction between the skills that are highest paid and those that are most in-demand. Data analysts aiming to maximise their career potential should consider developing a diverse skill set that includes both high-paying specialised skills and widely demanded foundational skills. 

## 4. What is the most optimal skill to learn for Data Analysts?

#### Visualise Data

``` python

from adjustText import adjust_text

sns.scatterplot(
    data=df_plot,
    x='skill_percent',
    y='median_salary',
    hue='technology'
)
plt.show()
```

#### Results

![Most Optimal Skills for Data Analysts in the US](3_Project/images/OptimalSkills_DA_US.png)
*A scatter plot visualising the most optimal skills (high paying & high demand) for data analysts in the US.*

#### Insights

- The scatter plot shows that most of the `programming` skills (coloured blue) tend to cluster at higher salary levels compared to other categories, indicating that programming expertise might offer greater salary benefits within the data analytics field.

- Analyst tools (coloured green), including Tableau and Power BI, are prevalent in job postings and offer competitive salaries, showing that visualisation and data analysis software are crucial for current data roles. This category not only has good salaries but is also versatile across different types of data tasks.

- The database skills (coloured orange), such as Oracle and SQL Server, are associated with some of the highest salaries among data analyst tools. This indicates a significent demand and valuation for data management and manipulation expertise in the industry. 

## What I Learned

Throughout this project, I deepened my understanding of the data analyst job market and enhanced my technical skills in Python, especially in data manipulation and visualisation. Here are a few specific things I learned:

* **Advanced Python Usage:** Utilising libraries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualisation, and other libraries helped me perform complex data analysis tasks more efficiently. 
* **Data Cleaning Importance:** I learned that thorough data cleaning and preparation are crucial before my analysis can be conducted, ensuring the accuracy of insights derived from the data. 
* **Strategic Skill Analysis:** The project emphasised the importance of alighning one's skills with market demand. Understanding the relationship between skill demand, salary, and job availability allows for more strategic career planning in the tech industry. 

## Insights

This project provided several general insights into the data job market for analysts:

* **Skill Demand and Salary Correlation:** There is a clear correlation between the demand for specific skills and the salaries these skills command. Advanced and specialised skills like Python and Oracle often lead to higher salaries. 
* **Market Trends:** There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Keeping up with these trends is essential for career growth in data analytics.
* **Economic Value of Skills:** Understanding which skills are both in-demand and well-compensated can guide data analysts in prioritising learning to maximise their economic returns. 

## Conclusion
This exploratioin into the data analyst job market has been incredibly informative, highlighting the critical skills and trends that shape this evolving field. The insights I got enhance my understanding and provide actionable guidance for anyone looking to advance their career in data analytics. As the market continues to change, ongoing analysis will be essential to stay ahead in data analytics. This project is a good foundation for future explorations and underscores the importance of continuous learning and adaptation in the data field. 