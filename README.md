# Project Overview  
🤔 Curious about the job market for Data Analysts? This project dives deep into the most valuable insights for aspiring Data Analysts, providing a clear picture of what’s currently in demand. This is a real-world, unguided project I built out of sheer curiosity 🔥, aimed at uncovering key trends and requirements for the Data Analyst role.

- 🔍 The insights focus on:
  - **Top-paying Data Analyst jobs**
  - **Key skills required in the industry**  
  - **Leading companies hiring Data Analysts**
  - **Monthly trends in job postings**
  - **In-demand technologies**, including:
    - Excel
    - SQL
    - Data Visualization tools (Power BI, Tableau)
    - Python

- SQL Queries? Check them out here : [project_sql folder]

# Background

This project stems from a growing interest in the Data Analyst field and the evolving job market. As organizations increasingly rely on data-driven decisions, understanding job trends and requirements is vital for aspiring analysts. By analyzing real-world data, I aimed to provide valuable insights that can guide future Data Analysts in their career paths.

- 🔗 **You can find datasets by clicking on this link:** [Project Datasets](https://drive.google.com/drive/folders/1moeWYoUtUklJO6NJdWo9OV8zWjRn0rjN)

## ⁉️ Questions I Aimed to Solve:
- What are the top-paying Data Analyst jobs available?
- Which skills are essential for landing these lucrative positions?
- What skills are currently most in demand for Data Analysts?
- Which companies are hiring for roles that require all five key Data Analyst skills, while also offering health benefits and remote work?
- How does the monthly trend of Data Analyst job postings change over time, particularly for positions requiring Python, Excel, SQL, Tableau, and Power BI?




# ⚙️ Tools I Used

- **PostgreSQL**: A powerful, open-source relational database management system that enables efficient data storage, retrieval, and complex queries for analyzing job market data.

- **Python**: A versatile programming language used for data analysis and visualization. Specifically, I utilized **Matplotlib** for creating insightful visual representations of job trends and requirements.

# The Analysis 

## Question 1: Which Data Analyst Roles Offer the Highest Salaries?
- Identify the top 10 highest paying Data Analyst positions available for remote work.
- Focus on job postings with specified salaries, ensuring null values are excluded.
- **Why?** Understanding the highest-paying opportunities helps aspiring Data Analysts target their career goals and enhances their knowledge of the job market.

```sql
SELECT
    job_id,
    job_title,
    job_location,
    job_schedule_type,
    salary_year_avg,
    job_posted_date,
    name AS company_name
FROM
    job_postings_fact f
LEFT JOIN 
    company_dim c 
ON 
    f.company_id = c.company_id     
WHERE
    job_title_short = 'Data Analyst' AND
    job_location = 'Anywhere' AND
    salary_year_avg IS NOT NULL
ORDER BY 
    salary_year_avg DESC
LIMIT 10;
```


# What I Learned 

# Conclusions
