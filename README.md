# Web-Scraping

## Project Overview
This project involved developing a web scraping solution to gather job postings from `CareerJet` web page based on user-defined search criteria.

The search criteria is based on `Job Position`, `Job Location` and `Number of Searched Pages`.

This project is done on Jupyter Notebook (`omedina_WebScraping.ipynb`) attached to this repository.

## Objective

"In order to improve job vacancy sourcing, the use of web scraping tools to extract job posting data from multiple sites provides a competitive advantage. This helps agencies provide their clients with relevant job openings more quickly."

## Careerjet Wep Page

Careerjet is a job search engine designed to simplify the process of finding employment opportunities online. It aggregates job listings from over 58,000 websites daily, including job boards, recruitment agency sites, and large specialist recruitment sites.

<img src="https://github.com/user-attachments/assets/724e5e97-8581-4c23-b20e-bbe52f180248" width="700">

## Web Scraping Tools

The goal was to scrape job postings for a given Job position and Job location, across multiple pages. The output should include relevant information such as `Job Title`, `Company`, `Job Location`, `Post Time`, `Extract Date`, `Salary`, and `Job URL`.

I used Python’s `requests` library to fetch the HTML content of the web pages and `BeautifulSoup` to parse the HTML and extract the required elements. The `csv module` was used to save the results to a CSV file. 

The CSV file is saved in the format: **"job_postings_`JobPosition`_`JobLocation` _`CurrentDate`.csv"**

## Function Breakdown

- `generate_url:` Generates the URL dynamically based on the input parameters (position, location, and page number).

```python
# Function to generate the URL based on position, location, and page
def generate_url(position, location, page=1):
    base_url = "https://www.careerjet.com/jobs"
    search_params = f"?s={position.replace(' ', '+')}&l={location.replace(' ', '+')}&p={page}"
    return base_url + search_params
```

- `scrape_jobs:` Scrapes job data from the generated URLs across multiple pages, processes the HTML, and writes the data to a CSV file.

  I also incorporated error handling and logging to track potential issues during scraping (e.g., page load failures or missing data).
  
```python
  # Function to scrape job postings based on position, location, and page
def scrape_jobs(position, location, pages):
    current_date = datetime.now().strftime("%Y-%m-%d")  # Get current date to timestamp the CSV file
    filename = f"job_postings_{position.replace(' ', '_')}_{location.replace(' ', '_')}_{current_date}.csv"
    
    # Open the CSV file for writing
    with open(filename, mode='w', newline='', encoding='utf-8') as file:
        writer = csv.writer(file)
        writer.writerow(['JobTitle', 'Company', 'JobLocation', 'PostTime', 'ExtractDate', 'Salary', 'JobURL'])  # Write the header row
        
        for page in range(1, pages + 1):
            url = generate_url(position, location, page)
            print(f'url page{page}: {url}')
            # Send a GET request to the generated URL
            response = requests.get(url)
            
            if response.status_code == 200:
                soup = BeautifulSoup(response.text, 'html.parser')
                job_listings = soup.find("ul", class_="jobs")  # Adjust selector based on actual page structure
                job_listings = job_listings.find_all('li', class_= lambda x: x != 'cjgad-outer') #extract job listings

                for job in job_listings:
                        
                    JobTitle = job.find('h2').find('a').text.strip() if job.find('h2') else None
    
                    company_tag = job.find('p', class_='company')
                    Company = company_tag.find('a').text.strip() if company_tag and company_tag.find('a') else None
                    
                    JobLocation = job.find('ul', class_='location').find('li').text.strip() if job.find('ul', class_='location') else None
                    
                    PostTime = job.find('footer').find('ul', class_='tags').find('li').find('span').text.strip() if job.find('footer') else None
                    
                    ExtractDate = datetime.now().strftime("%Y-%m-%d %H:%M")
                    
                    Salary = job.find('ul', class_='salary').find('li').text.strip() if job.find('ul', class_='salary') else None
                  
                    JobURL = "https://www.careerjet.com" + job.find('h2').find('a').get('href') if job.find('h2') else None
    
                    values =  [JobTitle, Company, JobLocation, PostTime, ExtractDate, Salary, JobURL]
                    if None not in values:
                        writer.writerow(values)
                                               
                # Introduce a delay between requests (avoid overloading the server)
                time.sleep(1)
            else:
                print(f"Failed to retrieve the page {page}. Status code: {response.status_code}")

    print(f"\nJob postings saved to {filename}")
```

## Testing the Code

- I tested the code with the following user-defined search criteria:

    Job Title:`Data Analyst`

    Job Location: `New York`

    Num of Searched Pages: `3`

 ```python
# Example usage
JobTitle = "Data Analyst"
Location = "New York"
Maxpages = 3

scrape_jobs(JobTitle, Location, Maxpages)
```
Output:

![image](https://github.com/user-attachments/assets/0329e30b-fbd7-489f-a47a-ec33ec8210e3)


- The code generated the CSV file `job_postings_Data_Analyst_New_York_2025-02-08.csv` with a total of 39 records out of 3 searched pages: 

![image](https://github.com/user-attachments/assets/f67d3a34-3e17-4bd9-8b4d-a820d87cadc6)

## Challenges Faced

- **Handling Missing Data:**

    Initially, I encountered issues with missing job details, such as company names and salaries. Some job postings did not have all the required data. To overcome     this, I added fallback logic that assigns `None` when specific fields are not found, ensuring the program doesn't crash.

- **Dynamic HTML Structure:**

    CareerJet’s HTML structure wasn’t uniform across all job postings, making it challenging to identify consistent tags for scraping. I used CSS classes like         `company`, `salary`, and `location`, which I tailored based on trial and error until I found the most reliable selectors.

- **Rate Limiting and IP Blocking:**

    To mitigate issues with rate limiting (where the server might block multiple requests in a short time), I introduced a `sleep delay` between requests. This           helped prevent the IP from being blocked for making too many requests too quickly.

## What Sets This Project Apart?

- **Error Handling and Robustness:**

  Unlike many beginner-level scrapers, I took steps to ensure the application doesn't fail if an expected field is missing. Using `if` checks allowed the scraper to handle edge cases smoothly.

- **Dynamic Page Handling:**

  The scraper can handle multiple pages by adjusting the URL query string dynamically, making it flexible for large data sets.

- **Clear Structure and Data Output:**

  The project outputs structured and clean data in CSV format, which can be used for further analysis or automated processes. The code is modular, making it easier to adapt for future use cases.

## Future Improvements

- **Improved Error Logging:**

  Future improvements could include adding more sophisticated logging, storing errors in a separate log file for easier debugging and monitoring.

- **Multithreading for Faster Scraping:**

  To speed up the scraping process, I could implement multithreading or multiprocessing, allowing multiple pages to be scraped concurrently. This would significantly reduce the time needed to collect data.

- **Scalability:**

  The scraper could be modified to handle large-scale scraping tasks, such as scraping data for multiple positions or locations in parallel. Integrating a database (e.g., SQLite or PostgreSQL) could allow storing 
  data for later analysis.
