# Web-Scraping

## Project Overview
This project involved developing a web scraping solution to gather job postings from `CareerJet` web page based on user-defined search criteria.

The search criteria is based on `Job position`, `Job location` and `Number of searched pages`.

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

## Function Breakdown

- `generate_url:` Generates the URL dynamically based on the input parameters (position, location, and page number).

    <img src="https://github.com/user-attachments/assets/431d00bc-f01f-43a2-a3b0-d1867a355c2a" width="700">

- `scrape_jobs:` Scrapes job data from the generated URLs across multiple pages, processes the HTML, and writes the data to a CSV file. I also incorporated error handling and logging to track potential issues during scraping (e.g., page load failures or missing data).
  
    <img src="https://github.com/user-attachments/assets/ea6b3e06-28d5-4871-b172-05173b4c0bba" width="700">

## Testing the Code

We tested the code with the following user-defined criteria:

Job Title:`Data Analyst`
Job Location: `New York`
Num of Searched Pages: `3`

<img src="https://github.com/user-attachments/assets/16b2a4f2-1453-4a5b-a012-87312ac1deb1" width="700">




  
