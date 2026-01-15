# Web Scraping NFL QB Data
I used Python to create the web scraper, with the help of GeeksforGeeks and Stack Overflow to guide my work. The data comes from the 2024 NFL season, and I used ESPN to web scrape. After completion, I ran the output through Stata to create confidence intervals and averages. The goals were to predict QB stats for the 2026 season, compare them to a season from 10 years ago, and track outlier performances.

## Requirements
- Python 3.7+
- Install dependencies: `pip install -r requirements.txt`

## Usage
1. Run the scraper: `python scraper.py`
2. The script will scrape the example URL (ESPN NFL QB passing stats) and print the table.
3. Data is also saved to `scraped_data.csv`.

## Customization
- Change the `url` variable in `scraper.py` to scrape different ESPN NFL stats pages.
- The script is designed for ESPN's NFL player stats pages.

## Dependencies
- requests: For HTTP requests
- beautifulsoup4: For HTML parsing
- pandas: For data manipulation and table display
- lxml: For faster HTML parsing
