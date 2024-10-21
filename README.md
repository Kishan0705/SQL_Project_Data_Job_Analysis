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


### 📝 Insights

- **SQL**: Dominates the market with **92,628** job postings. This skill is essential for data retrieval and management.

- **Excel**: A staple in **67,031** job listings. Its stronghold lies in data analysis and spreadsheet management.

- **Python**: Found in **57,326** postings, highlighting its importance in data analysis and automation tasks.

- **Tableau**: Featured in **46,554** job ads. This tool is pivotal for transforming data into impactful visual stories.

- **Power BI**: Present in **39,468** job listings. It's increasingly valuable for creating interactive dashboards and reports.

## 🔍 Question 2: Identify the companies that have posted job listings requiring all top 5 skills for "Data Analyst" positions, while offering health insurance and work-from-home options.

- **Condition 1**: Offering **health insurance**.
- **Condition 2**: Providing **work-from-home options**.

```sql
WITH top_skills AS (
    SELECT
        s.skill_id,
        s.skills
    FROM skills_dim s
    JOIN skills_job_dim sj ON s.skill_id = sj.skill_id
    JOIN job_postings_fact f ON sj.job_id = f.job_id
    WHERE f.job_title_short = 'Data Analyst' 
      AND f.job_health_insurance = 'TRUE'
      AND f.job_work_from_home = 'TRUE'
    GROUP BY s.skill_id, s.skills
    ORDER BY COUNT(f.job_id) DESC
    LIMIT 5
),
jobs_with_all_skills AS (
    SELECT f.job_id, f.company_id
    FROM job_postings_fact f
    JOIN skills_job_dim sj ON f.job_id = sj.job_id
    JOIN top_skills ts ON ts.skill_id = sj.skill_id
    GROUP BY f.job_id, f.company_id
    HAVING COUNT(DISTINCT ts.skill_id) = 5  -- Only jobs that require all 5 skills
)
SELECT
    c.name AS company_name,
    COUNT(jwa.job_id) AS Jobs_Requiring_All_Skills
FROM jobs_with_all_skills jwa
JOIN company_dim c ON jwa.company_id = c.company_id
GROUP BY c.name
ORDER BY Jobs_Requiring_All_Skills DESC
LIMIT 10;
```

![Top 10 Most Companies Required All 5 Skills for DA Roles Visualization](https://github.com/Kishan0705/SQL_Project_Data_Job_Analysis/blob/45c59cd05daf87b5adf3bc883c10197010a7825c/assets/Top%20Com%20Req%20DA%205%20Skills.png)

## 📝 Insights on Companies Requiring All 5 Skills for Data Analyst Roles

- **Walmart**: Leads the pack with **172 job openings**, highlighting its commitment to finding well-rounded Data Analysts who can handle diverse analytical tasks.

- **Agoda**: With **155 postings**, this travel platform is keen on professionals equipped with essential skills to optimize data-driven decisions in a competitive market.

- **Guidehouse**: Boasts **124 positions** that seek analysts capable of navigating complex datasets, showcasing the company's focus on innovative solutions.

- **Epsilon**: Offers **84 job opportunities** for Data Analysts, emphasizing their need for skilled individuals who can enhance their marketing analytics capabilities.

- **Citi**: With **80 openings**, Citi is on the lookout for Data Analysts who can contribute to their data strategy and financial analytics efforts.

- **Listopro**: Has **68 job listings**, indicating a strong demand for skilled analysts to support their operational and strategic initiatives.

- **Navy Federal Credit Union**: With **63 postings**, this organization values Data Analysts who can manage and interpret financial data effectively.

- **Deloitte**: Offers **54 job openings**, seeking analysts who can deliver insights that drive business transformation and client success.

- **Visa**: With **53 job listings**, Visa looks for analytical talent to enhance its data-driven approach in the financial technology sector.

- **CBRE**: Also has **53 positions**, reflecting the need for Data Analysts who can interpret real estate market trends and data.

  ##  🔍 Question 3: Monthly Growth of Data Analyst Job Postings

The following SQL query analyzes the monthly growth of job postings for Data Analysts, highlighting both the number of jobs posted and the monthly changes.

```sql
SELECT
    EXTRACT(MONTH FROM job_posted_date) AS Month_number,  
    EXTRACT(YEAR FROM job_posted_date) AS Years,
    TO_CHAR(job_posted_date, 'Month') AS Month_name,    
    COUNT(job_id) AS No_of_jobs,
    COUNT(job_id) - LAG(COUNT(job_id)) OVER (
        ORDER BY EXTRACT(YEAR FROM job_posted_date), EXTRACT(MONTH FROM job_posted_date)
    ) AS Difference
FROM 
    job_postings_fact 
WHERE 
    job_title_short = 'Data Analyst' 
GROUP BY 
    Month_name, Years, Month_number  
ORDER BY 
    Years ASC, Month_number ASC;
```

![Monthly Growth of Data Analyst Job Postings Visualization](https://github.com/Kishan0705/SQL_Project_Data_Job_Analysis/blob/96e96104c7eab39c03e191372ceac57a6df2a7ac/assets/Monthly%20Growth%20of%20Data%20Analyst%20Job%20Postings%20.png)

# What I Learned 

# Conclusions
