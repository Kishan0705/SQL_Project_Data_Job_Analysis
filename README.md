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
## 🔍 Question 1: What are the Most In-Demand Skills for Data Analysts?

- **Objective**: Identify the top 5 most sought-after skills for Data Analyst roles based on the number of job postings requiring them.
- **Why?**: Knowing the most in-demand skills helps aspiring Data Analysts prioritize their learning and improve their job prospects.

```sql
SELECT
    s.skills,
    COUNT(sj.job_id) AS Total_Jobs
FROM 
    job_postings_fact f
JOIN 
    skills_job_dim sj ON f.job_id = sj.job_id
JOIN 
    skills_dim s ON s.skill_id = sj.skill_id
WHERE 
    f.job_title_short = 'Data Analyst'
GROUP BY 
    s.skills
ORDER BY 
    Total_Jobs DESC
LIMIT 5;
```
![Top 5 Most Demanded Data Analyst skills Visualization](https://github.com/Kishan0705/SQL_Project_Data_Job_Analysis/blob/efb2bbe76b3b9c3b1ef34df4a2eb39c3e4d04bcb/assets/Top%205%20DA%20Skills%20.png)

### 📊 Insights

- **SQL**: Dominates the market with **92,628** job postings. This skill is essential for data retrieval and management.

- **Excel**: A staple in **67,031** job listings. Its stronghold lies in data analysis and spreadsheet management.

- **Python**: Found in **57,326** postings, highlighting its importance in data analysis and automation tasks.

- **Tableau**: Featured in **46,554** job ads. This tool is pivotal for transforming data into impactful visual stories.

- **Power BI**: Present in **39,468** job listings. It's increasingly valuable for creating interactive dashboards and reports.



# What I Learned 

# Conclusions
