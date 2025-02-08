# Web-Scraping

## Project Overview
This project involved developing a web scraping solution to gather job postings from CareerJet based on user-defined search criteria.

The search criteria is based on `Job position`, `Job location` and `Number of pages`.

This project is done on Jupyter Notebook (`omedina_WebScraping.ipynb`)

## Objective

"In order to improve job vacancy sourcing, the use of web scraping tools to extract job posting data from multiple sites provides a competitive advantage. This helps agencies provide their clients with relevant job openings more quickly."

## Careerjet Wep Page

Careerjet is a job search engine designed to simplify the process of finding employment opportunities online. It aggregates job listings from over 58,000 websites daily, including job boards, recruitment agency sites, and large specialist recruitment sites.

<img src="https://github.com/user-attachments/assets/724e5e97-8581-4c23-b20e-bbe52f180248" width="700">

## Web Scraping Tools

The goal was to scrape job postings for a given Job position and Job location, across multiple pages. The output should include relevant information such as job Title, Company, Job Location, Salary, Posting Time, and Job Post URL.

I used Python’s `requests` library to fetch the HTML content of the web pages and `BeautifulSoup` to parse the HTML and extract the required elements. The `csv module` was used to save the results to a CSV file. 

The CSV file is saved in the format: job_postings_`JobPosition`_`JobLocation` _`CurrentDate`.csv"

  
### Data Visualization
- 📊 **Histogram of Likes** revealed the overall engagement distribution across posts.
- 📌 **Boxplot of Likes per Category** highlighted which content types received more likes.
- Choosing the best visualization was a challenge, but testing different graphs helped identify the most informative ones.

<img src="https://github.com/user-attachments/assets/6a561ed3-e580-4344-8912-0ea62f03da49" width="400">
<img src="https://github.com/user-attachments/assets/70cb0073-15a8-4e28-a785-b7d310d0373c" width="400">

### Statistical Analysis & Insights
- The **average number of likes per post** was **~5000**.
- **Food, Fashion, and Fitness** categories received the highest engagement, indicating users prefer these content types.
- **Travel and Culture** posts had lower engagement, suggesting they might require better captions, hashtags, or posting times to improve reach.

![image](https://github.com/user-attachments/assets/73c40af6-b891-43bc-9c22-8b0ce7e1e2e2)


## What Sets This Project Apart?
✅ **Realistic Instagram Analytics Simulation**: The dataset structure mirrors real social media insights, making the analysis practical for businesses.  
✅ **Actionable Insights for Social Media Strategy**: Helps brands & influencers decide which content types to focus on.  
✅ **End-to-End Data Pipeline**: Covers data generation, cleaning, visualization, and analysis in a single project.  

## Future Improvements & Business Applications
📊 **Time-Based Analysis**: Study engagement trends based on posting time & day of the week.  
🤖 **Machine Learning for Prediction**: Predict which posts will go viral based on category and past likes.  
📈 **Deeper Instagram Metrics**: Extend analysis to comments, shares, and follower growth for richer insights.  
